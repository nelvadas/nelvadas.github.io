## Getting Started with DTrace on Oracle linux

DTrace (Dynamic Tracing) is a powerful, open-source framework designed for real-time diagnostics and performance analysis of both operating systems and applications. Originally developed by Sun Microsystems for the Solaris operating system, DTrace has since been ported to various platforms, including macOS, FreeBSD, Windows, and Linux. 

It is pratical for 
* performance tuning, identifying and resolve performance bottleneck in applications
* Debugging : trace systemcall, function execution to diagnose bugs
* Security Analysis : 
* Resource Monitoting : 



---

### Installation

#### Install DTrace 

```bash

[opc@olam-server-01 ~]sudo dnf config-manager --enable ol8_UEKR7



```

#### Installation Checks 

DTrace Location 
```sh
[opc@olam-server-01 ~]$ which dtrace
/usr/sbin/dtrace
```


DTrace Version
```sh
[opc@olam-server-01 ~]$ dtrace -V
dtrace: Oracle D 2.0

```

#### DTrace HelloWorld

Print a helloworld inline program

```sh
[opc@olam-server-01 ~]$ sudo dtrace -n 'BEGIN {printf("helloworld\n");}'
dtrace: description 'BEGIN ' matched 1 probe
CPU     ID                    FUNCTION:NAME
  3      1                           :BEGIN helloworld
````



Print a helloworld script program

```sh
[opc@olam-server-01 ~]$ cat hellodtrace.d
BEGIN {printf("helloworld\n");}
[opc@olam-server-01 ~]$ sudo dtrace -s hellodtrace.d
dtrace: script 'hellodtrace.d' matched 1 probe
CPU     ID                    FUNCTION:NAME
  2      1                           :BEGIN helloworld


```


### Probes and Providers
Probes are event that may be tracked on your linux system

```md
provider:module:function:name 
```

example
```md
syscall:vmlinux:bind:entry
````

Count the probes available on your system

```sh 
[opc@olam-server-01 ~]$ sudo dtrace -l | wc -l
225189
[opc@olam-server-01 ~]$
```

Displaying some probes 

```sh
[opc@olam-server-01 ~]$ sudo dtrace -l | head -10
   ID   PROVIDER            MODULE                          FUNCTION NAME
    1     dtrace                                                     BEGIN
    2     dtrace                                                     END
    3     dtrace                                                     ERROR
    4        cpc                                                     unhalted_core_cycles-all-1000000000
    5        cpc                                                     instruction_retired-all-1000000000
    6        cpc                                                     unhalted_reference_cycles-all-1000000000
    7        cpc                                                     llc_references-all-1000000000
    8        cpc                                                     llc_misses-all-1000000000
    9        cpc                                                     branch_instructions_retired-all-1000000000
```

### D probes 


