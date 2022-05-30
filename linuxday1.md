# 50daysofLinux - Day 1 Navigation Commands


## Introduction

Today my notes are about the navigation commands found in Linux. We learn to locate, view and create files within the Linux file system.

If you want to know more about installing Linux, then please use [This article](https://www.exploreazure.co.uk/projects/linux/post1). 

## Navigation Commands

The Linux file system follows a tree-like hierarchial structure. However, the tree is upside down, as the root is the top-level directory.


To list files and directories use ls

```
ls
```

The -l option will output in long listing format, as the default will only show the names of the files. The long listing format is much more helpful.

```
ls -l
```

In Linux there are hidden files, they have prefixed with a fullstop to show hidden files use ls -a. The below command combines the log listing option and hidden files option:

![ls -al command](https://i.imgur.com/cYOF9sK.png)

The ls -d */ will show directories only. This article provides more details about the [ls command](https://linuxize.com/post/how-to-list-files-in-linux-using-the-ls-command/)


As you can see, each command has a number of options. When just starting out with Linux, it is difficult to remember all these options. Overtime you will remember the common options. However, the Linux help system will be your friend, when searching for a new command or command option. This article provides more details about the [help system](https://www.exploreazure.co.uk/projects/linux/post2/getting-help). 


**To change directories use the cd**

cd (change directory) - Is used to change levels within the Linux directory structure.

You can use absolute or relative path names.

An absolute pathname would look like this:

```
cd /var/log
```
The absolute path or full path will start with the system root /

Alternatively, you can use relative paths. Absolute paths always start at the system root (/). Relative paths start from the current working directory. The ```pwd``` command, will show your current location within the Linux directory structure. 


Here are some relative path examples to remember:


```
# Display the working directory
pwd
# Output /var/log

# Move up one level (.. represents parent directory)
cd ..
## current working directory is now /var

cd ./log
## current working directory is now /var/log (. represents current working directory)

cd ../..
# current working directory is now / (system root)

cd -
# current working directory is now  /var/log (- will change to previous directory)

cd ~
# current working directory is now /home/barry (~ will change to your home directory, in my case /home/barry)

```

## Viewing File Contents

To view all the contents in the file, use the cat command:

```
cat /var/log/syslog
```

To display one page at a time, use the more command:

```
more /var/log/syslog
# press space bar to display next page, or q to exit
```

The less command is similar to the more command, as it displays the file contents a page at a time. However, you can use the following features:

/search-for-word - You can search for text using the / character
Enter - You can navigate line by line, by pressing enter
Page Up / Page down - To navigate page by page in either direction

```
less /var/log/syslog
# faster than more, as it doesn't load all the file contents into memory
```

## Getting information about file

The stat command provides statistics about a file

![stat command](https://i.imgur.com/wjSWtMg.png)

This is useful for finding information about file type, size and permissions. However, normally the ls command is used to find out this type of information. The stat command is useful when working with symlinks. Currently, creating an article about symlinks, this will be published shortly.

## Conclusion

This article provides information on how to navigate up and down the Linux file system. The next section describes some ways to view the contents of a text file. 
 