# Is Docker really secure?

This article deals with the notion of security with Docker containers. While Docker has proved to be a boon for easing out deployment 
time and resources and significantly reduced compatibility problems, a lot needs to be discovered for securing the container environment.  
Security concerned with Docker is not only limited to just securing the containers instantiated, but also to make sure that users
who have container access are not able to interrupt with the host system at any cost.

## Docker Security - Present Mindset

Most Docker users argue that Docker containers are secure as they are isolated and do not interrupt with the processes running on the host or on other containers.
This argument is based on the fact that Docker uses the Linux namespaces and cgroups. 

There are numerous ways in which Docker containers have exploited the security parameters. One such way is described in this post - <b> Bypassing the Audit checks by Linux </b>.

Before beginning, let's throw some light on what auditing is.

## Audit Feature in Linux

<b> audit </b> is an interesting security feature of the Linux kernel. Auditing helps the system administrators to trace every action on the Linux system by the means of logging. This trace is called an <b> audit trail </b>. We can track security-relevant events, record the events in a log file, and detect misuse of resources/data or unauthorized activities by inspecting the audit log files. Logging of events is generally done in a specific file called <b> audit.log</b>.

Audit does not provide additional security to your system, rather, it helps track any violations of system policies and enables you to take additional security measures to prevent them.

<b>auditd</b> is the Audit Daemon for Linux.

In a Ubuntu-based system, this package can be downloaded as such:

```
# apt install auditd
```
![Install auditd](https://github.com/Prashansa-K/Docker/blob/master/Security/auditd-running.PNG)

The service of auditd should automatically start. If it doesn't use the following commands:

```
# systemctl start auditd
# systemctl status auditd
```
![View the Auditd service Running](https://github.com/Prashansa-K/Docker/blob/master/Security/auditd-running.PNG)
Now, let's create a audit trail for /etc/shadow file. This is one of the most critical Linux files, as it saves the passwords of all Linux users. Though the passwords saved are hashed, it is essential to keep this file from getting compromised.

```
# auditctl -w /etc/shadow
```

This command inserts a 'watch' for the file /etc/shadow and would trace accesses or changes being done to the file.


## Creating Audit Trails

Now, let's try to modify this file - or just update the timestamp on it to experiment.

```
# touch /etc/shadow
```

To check the audit trail now, use `ausearch` command as such:

```
# ausearch -f /etc/shadow -i -ts recent
```

`ausearch` is a tool to query audit daemon logs. The option `-f` helps us to search for audit events for the filename specified. 
The option `-i` is used to resolve the UID into usernames. `-ts` option allows us to add timestamps to filter events. You can specify proper timestamps or just use keywords like <b> today, now, recent, yesterday, this-week, etc. </b>

![Audit Trail produced when root 'touched' the /etc/shadow file](https://github.com/Prashansa-K/Docker/blob/master/Security/ausearch-shadow.PNG)

As you can see in the image, the uid and gid correspond to 'root'. But, auid (Audit UID) shows 'prashansa'. This is because I initially logged in as 'prashansa' user (not an administrative user) and then switched to root using 'su - root' command.
Thus, the trail clearly depicts that initial process is owned by 'prashansa' user and /etc/shadow file is modified with the power of 'root' user.

We can also touch the file from 'prashansa' user and check the audit trails again.

![Audit trails after prashansa user 'touched' /etc/shadow file](https://github.com/Prashansa-K/Docker/blob/master/Security/ausearch-with-onlyprash.png)

In this image, you can see that auid, uid and gid all point to 'prashansa' user.

## How does this tracking occur?

There is a field called loginuid, stored in /proc/self/loginuid, that is part of the proc struct of every process on the system. This field can be set only once; after it is set, the kernel will not allow any process to reset it.

So, whichever user you become using su command, this id will remain same.

```
# cat /proc/self/loginuid
```

Below images clearly depict that loginuid of both root and prashansa is 1000.

![loginuid of root]()

![loginuid of prashansa user]()


Every process that is forked and executed from the initial login process automatically inherits this loginuid. This is how Linux kernel identifies that the person who logged was 'prashansa' user.

Now, let's jump to Docker containers and see how they use this feature.

## Docker Containers and Auditing
