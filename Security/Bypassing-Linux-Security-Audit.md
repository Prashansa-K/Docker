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
$ apt install auditd
```
![]
