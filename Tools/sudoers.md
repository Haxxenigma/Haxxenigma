# [Sudoers](https://help.ubuntu.com/community/Sudoers)

## Choose editor:

```shell
sudo select-editor
```

OR

## ~/.bashrc:

```shell
export EDITOR="nano"
```

## Edit sudoers file:

```shell
sudo visudo
```

## Users privileges:

```
root ALL=(ALL:ALL) ALL {
    The first field shows the username that the rule will apply to (root).

    The first “ALL” means that this rule applies to all hosts.

    Second “ALL” means that the root user can run commands on behalf of all users.

    Third “ALL” means that the root user can run commands on behalf of all groups.

    The last “ALL” means that these rules apply to all commands.
}
```

## Add user to sudoers:

```shell
sudo usermod -aG sudo username
```

OR

```shell
sudo gpasswd -a username sudo
```

OR

## /etc/sudoers:

```shell
%sudo   ALL=(ALL:ALL) ALL, username
```

## Check configuration:

```shell
sudo visudo -c
```