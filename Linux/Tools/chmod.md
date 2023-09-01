# [Chmod](https://ru.wikipedia.org/wiki/Chmod "https://ru.wikipedia.org/wiki/Chmod")

```
chmod [options] <ugoa+-=rwxXst | 000-777> <path/to/file>
```

***TARGET***

| Reference | Class   | Description                                                            |
| :-------- | :------ | :--------------------------------------------------------------------- |
| u         | user    | file owner                                                             |
| g         | group   | members of the file's group                                            |
| o         | others  | users who are neither the file's owner nor members of the file's group |
| a         | all     | all three of the above, same as ugo                                    |
| (empty)   | default | same as "all", except that bits in the umask will be unchanged         |

***PERMISSIONS***

| Mode | Name            | Description                                                                                                                                                                                    |
| :--- | :-------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| r    | read            | read a file or list a directory's contents                                                                                                                                                     |
| w    | write           | write to a file or directory                                                                                                                                                                   |
| x    | execute         | execute a file or recurse a directory tree                                                                                                                                                     |
| X    | special execute | applies execute permissions to directories regardless of their current permissions and applies execute permissions to a file which already has at least one execute permission bit already set |
| s    | setuid/gid      | [setuid/gid](https://en.wikipedia.org/wiki/Setuid "https://en.wikipedia.org/wiki/Setuid")                                                                                                      |
| t    | sticky          | [sticky bit](https://en.wikipedia.org/wiki/Sticky_bit "https://en.wikipedia.org/wiki/Sticky_bit")                                                                                              |

***NUMERICAl PERMISSIONS***

| #    | rwx  | Permission              |
| :--- | :--- | :---------------------- |
| 0    | ---  | none                    |
| 1    | --x  | execute only            |
| 2    | -w-  | write only              |
| 3    | -wx  | write and execute       |
| 4    | r--  | read only               |
| 5    | r-x  | read and execute        |
| 6    | rw-  | read and write          |
| 7    | rwx  | read, write and execute |
| 4000 | u+s  | SUID                    |
| 2000 | g+s  | SGID                    |
| 1000 | +t   | sticky bit              |