# 50daysofLinux - Day 2 Sudo

## Introduction
Some system commands require root privileges to execute. ```sudo``` is used to run a command with the security privileges of another user. This avoids a permission denied error.

This article describes how and when to use sudo. 

It also explains how you can safely update the /etc/sudoers file to make configuration changes.

## Name
The name stands for SuperUser DO, as by default the sudo will try to run the command under the root account. 

As you can switch to any user, some people prefer the Substitute User DO name. The SuperUser DO is the formal name given by its maintainers.

## What sudo can do?

On your Linux system, try the following commands:

```
cd /
touch pleaseremove1.tmp
```

The above cd command will change directory to the top-level root directory. The touch command will try to create an empty file called pleaseremove1.tmp.

The root directory is commonly protected, which will result in a permission denied error message.


To create a file at the root directory, try this:

```
cd /
sudo touch pleaseremove1.tmp
ls -l *.tmp
```

When you prefix the command with sudo, it will by default run the command using root privileges.

You will be prompted to enter your user password, as a security measure.

The file is created under the root directory without error, as the sudo prefix is running the touch command under the root user context. 

The -i can be used to run multiple commands under the root context 

```
sudo -i
```
Use exit to return to your user context.

**Helpful tip**
I am always forgetting to add sudo infront of a command which requires root permissions. To save some typing you can run the previous by using the !! shortcut:

```
useradd bob
# oops, a permission denied error is returned, as I forgot the sudo prefix
sudo !!
# this will run the previous command, including the sudo prefix
# saves me time :-)
```

As you can see the sudo command is a powerful prefix to add to a command. Not all users can use this powerful ability. In the next section, we will look at the configuration files associated to sudo.


## sudo configuration files

The main sudo configuration is normally found at /etc/sudoers.  **Do not edit this using a text editor, use the following command:**

```
sudo visudo
```
The first time you use the visudo command, you may be prompted to select your preferred text editor. Use this command if you want to change your text editor selection at a later date:

```
sudo select-editor
```

The two key concepts we need to learn to understand the sudoers file format are:

1. Aliases
2. User privileges specification

### Alias

Let's begin with the alias concept. You can create an alias to create a list of one of more users, hosts or commands. Lets use an example to learn more about aliases in the sudoers file.

If you are following along, please run the following command again:

```
sudo visudo
```
Move under the Cmd alias specification command and add the following line:

```
Cmnd_Alias USER_ADMINS_CMDS = /usr/sbin/passwd, /usr/sbin/useradd, /usr/sbin/userdel, /usr/sbin/usermod
```

Now move down to the user privilege specification section and add:

```
useradmin1 ALL=(ALL:ALL) USER_ADMINS_CMDS 
```

You can write and quit from your favourite text editor to save changes.

**So what have we just done?**

We have created an alias called USER_ADMIN_CMDS, useradmin1 can now use the sudo command to execute the useradmin commands. The useradmin1 user is prevented from running other root commands, such as removing files owned by root.

Let's test to see if this sudoers change has worked. In my case, I do not have a user on my system called useradmin1. In my lab environment, I have created this user:

```
sudo adduser useradmin1
```
This has created a new user, you will need to enter a password, you can press enter to skip the other prompts.


Let's switch user to useradmin1 by:

```
sudo su - useradmin1
```

Now, we try to delete the file we created in the first section of this article:

```
cd /
sudo rm pleaseremove1.tmp
```

You should be prevented from deleting the file, as useradmin1 is not allowed to execute the rm command in the root context.

Whilst, still within the useradmin1 context, let's try to modify the useradmin1 user by adding a comment to its profile:

```
sudo usermod useradmin1 -c "temp user"
```

As the usermod command is listed in the sudoers file, the command is allowed to execute. 

### User privilleges specification 

The format to specify a user privilege is:

```
<user> <host> (<accounts>:<groups>) <tag list> <commands>
```

Let's look at some examples to understand this format:

```
root ALL=(ALL:ALL) ALL
```

This line states the root user can run commands on all hosts (sudoers can be shared across systems, this value is commonly set to ALL). The brackets surrounding the two ALL values will allow the root user to execute commands as any user/group. The final ALL value, allows sudo to run any command.

In summary, the first example means the root user from all hosts from any account can run all commands.

In the next example, we restrict what sudo can execute, before editing the sudoers file. I have created the following group:

```
sudo addgroup useradmins
```

Next, I used the ```sudo visudo``` command and inserted the below lines:

```
# Members of the useradmins group may gain root privileges and execute user admin commands
%useradmins ALL=(ALL:ALL) USER_ADMINS_CMDS
```

In this example, the % indicates a group name. The alias USER_ADMINS_CMDS was defined and explained in a previous section.

Our final example shows the use of a tag within a user privilege line:

```
useradmin2 ALL=(ALL:ALL) NOPASSWD: USER_ADMINS_CMDS
```

This example uses the optional tag example. Which suppresses the password prompt

## Tidy up

If you want to tidy up your system, you can remove the file and the account using the below commands:

```
cd /
sudo rm pleaseremove1.tmp
sudo userdel useradmin1
```

You can also remove the lines in the sudoers files, which were added whilst following along with the examples in this article (remember to use ``` sudo visudo ```).

## Summary

As you can see, you gain great power when you elevate your permissions using sudo. The sudoers configuration file is very useful when tailoring the power of sudo to meet the needs of your administrators. 

## Resources

[Ubuntu SUDO help article](https://help.ubuntu.com/community/Sudoers)

[Linux Crash Course - Sudo (Youtube)](https://www.youtube.com/watch?v=07JOqKOBRnU)
