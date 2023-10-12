# [Metasploit](https://www.kali.org/tools/metasploit-framework/)

## Useful commands

```shell
help [command]
```

```shell
search [options] [keywords:value]
```

```shell
info <module name>
```

```shell
use <module name>
```

```shell
show [all | encoders | nops | exploits | payloads | auxiliary | post | plugins | info | options | favorites | missing | advanced | evasion | targets | actions]
```

```shell
set [-c, --clear(unset) | -g, --global(setg)] [name] [value]
```

```shell
exploit | run
```

```shell
background | Ctrl+Z
```

```shell
sessions [-i]
```

```shell
back
```

## Main Components of Metasploit

> /usr/share/metasploit-framework/modules

```
├── auxiliary
├── encoders
├── evasion
├── exploits
├── nops
├── payloads
└── post
```

### [Auxiliary](https://unclesp1d3r.github.io/posts/2023/03/metasploit-framework-an-overview-of-the-open-source-penetration-testing-tool/#auxiliary-modules)

Any supporting module, such as scanners, crawlers and fuzzers.

### [Encoders](https://unclesp1d3r.github.io/posts/2023/03/metasploit-framework-an-overview-of-the-open-source-penetration-testing-tool/#encoders)

Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.

Signature-based antivirus and security solutions have a database of known threats. They detect threats by comparing suspicious files to this database and raise an alert if there is a match. Thus encoders can have a limited success rate as antivirus solutions can perform additional checks.

### [Evasion](https://www.hackers-arise.com/post/2019/03/27/metasploit-basics-for-hackers-part-24-the-new-evasion-modules-in-metasploit-5)

While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, “evasion” modules will try that, with more or less success.

### [Exploits](https://unclesp1d3r.github.io/posts/2023/03/metasploit-framework-an-overview-of-the-open-source-penetration-testing-tool/#exploit-modules)

A piece of code that uses a vulnerability present on the target system.

### [NOPs](https://unclesp1d3r.github.io/posts/2023/03/metasploit-framework-an-overview-of-the-open-source-penetration-testing-tool/#no-operation-nop-modules)

NOPs (No OPeration) do nothing, literally. They are represented in the Intel x86 CPU family they are represented with 0x90, following which the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes.

### [Payloads](https://unclesp1d3r.github.io/posts/2023/03/metasploit-framework-an-overview-of-the-open-source-penetration-testing-tool/#payload-modules)

Payloads are codes that will run on the target system.

Exploits will leverage a vulnerability on the target system, but to achieve the desired result, we will need a payload. Examples could be; getting a shell, loading a malware or backdoor to the target system, running a command, or launching calc.exe as a proof of concept to add to the penetration test report. Starting the calculator on the target system remotely by launching the calc.exe application is a benign way to show that we can run commands on the target system.

Running command on the target system is already an important step but having an interactive connection that allows you to type commands that will be executed on the target system is better. Such an interactive command line is called a "shell". Metasploit offers the ability to send different payloads that can open shells on the target system.

You will see four different directories under payloads: adapters, singles, stagers and stages:

1. Adapters: An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.
2. Singles: Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.
3. Stagers: Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.
4. Stages: Downloaded by the stager. This will allow you to use larger sized payloads.

Metasploit has a subtle way to help you identify single (also called “inline”) payloads and staged payloads.

1. generic/shell_reverse_tcp
2. windows/x64/shell/reverse_tcp

Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the “_” between “shell” and “reverse”. While the latter is a staged payload, as indicated by the “/” between “shell” and “reverse”.

### [Post](https://unclesp1d3r.github.io/posts/2023/03/metasploit-framework-an-overview-of-the-open-source-penetration-testing-tool/#post-exploitation-modules)

Post modules will be useful on the final stage of the penetration testing process, post-exploitation.

## Parameters you will often use are

1. RHOSTS: “Remote host”, the IP address of the target system. A single IP address or a network range can be set. This will support the CIDR (Classless Inter-Domain Routing) notation (/24, /16, etc.) or a network range (10.10.10.x – 10.10.10.y). You can also use a file where targets are listed, one target per line using file:/path/of/the/target_file.txt.
2. RPORT: “Remote port”, the port on the target system the vulnerable application is running on.
3. PAYLOAD: The payload you will use with the exploit.
4. LHOST: “Localhost”, the attacking machine IP address.
5. LPORT: “Local port”, the port you will use for the reverse shell to connect back to. This is a port on your attacking machine, and you can set it to any port not used by any other application.
6. SESSION: Each connection established to the target system using Metasploit will have a session ID. You will use this with post-exploitation modules that will connect to the target system using an existing connection.