# Sudo logging

Arguibly the most important job as a sysadmin is to check sudo who, where, when and what.
This is one of the more easier ones as its really just adding 3 lines to a single file.

## sudo visduo

```sudo visudo```, memorize this! Because you will go to this file a bunch of times.
This opens the sudoers file with the default editor and will look something like this:

![port](/images/sudo.png)

This is where you will do the:
- Requirement for TTY
- Restricting sudo to the specified directories
- Re-directing the logging for sudo
- Set the bad password message & attempts

To log our sudos add these rules, the IO logdir has to be that what the subject specifies in my case its ```/var/log/sudo/```.

```shell
Defaults	log_output
Defaults	log_input
Defaults	iolog_dir=/var/log/sudo/
```

## The directories
When we do this then for **EVERY** sudo command that gets executed a new directory is created, which contains the following files:

![port](/images/sudo2.png)

## The actual logging part

Here we can see what is what when we do ```cat log```:

![port](/images/sudo3.png)
