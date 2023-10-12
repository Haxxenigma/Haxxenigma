# [Hydra](https://github.com/vanhauser-thc/thc-hydra)

```
hydra [[[-l LOGIN|-L FILE] [-p PASS|-P FILE]] | [-C FILE]] [-e nsr] [-o FILE] [-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-W TIME] [-f] [-s PORT] [-x MIN:MAX:CHARSET] [-c TIME] [-ISOuvVd46] [-m MODULE_OPT] [service://server[:PORT][/OPT]
```

## Options:

`-l LOGIN` or `-L FILE`: login with LOGIN name, or load several logins from FILE

`-p PASS`  or `-P FILE`: try password PASS, or load several passwords from FILE

`-C FILE`: colon separated "login:pass" format, instead of -L/-P options

`-M FILE`: list of servers to attack, one entry per line, ':' to specify port

`-t TASKS`: run TASKS number of connects in parallel per target (default: 16)

`-m OPT`: options specific for a module, see -U output for information

## FTP:

```shell
hydra -l <username> -P <wordlist> ftp://<IP-address>
```

## SSH:

```shell
hydra -l <username> -P <wordlist> ssh://<IP-address> -t 4
```

```shell
hydra -l <username> -P <wordlist> <IP-address> -t 4 ssh
```

## Post Web Form:

```shell
hydra -l <username> -P <wordlist> <IP-address> http-post-form "<path>:<login_credentials>:<invalid_response>"
```

```shell
hydra -l admin -P rockyou.txt 10.10.1.64 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
```