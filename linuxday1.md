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



 