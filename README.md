# zig-select
Small zig version selection utility. zig-select will manage your ZIG installations in your home directory. It is written with the focus on being efficient, self explaining, and to keep multiple 
installations of zig in a proper place.

## About

zig-select is a small utility written in bash to easily switch between different versions of zig. 
It should work on any GNU/linux system. On mac osx in theory it should also work, but I did not
verify that yet.  
I wrote this utility mainly for myself, please see the gist [Managing multiple versions of ZIG on your system easily](https://gist.github.com/M64GitHub/6d2e0cedb69edd9041c92e1422d9f6b6) to find out more to why and how the following prerequisites, and modus operandus were chosen:  

The script will expect and handle your extracted binary downloads of the zig language for your
system. In order to achieve still a bit of flexibility, it works with directory names, at least
for now:

## Installation / System Setup
- Just download the script and make it executable. The script will manage your installations by creating the following directory structure if it does not exist yet (you can also do this yourself, manually):
```
~/ZIG
~/ZIG/_downloads/
```

- Run the script a first time to create the directories for you:
```
❯ ./zig-select
Creating ZIG root directory /home/m64/ZIG ...
Creating ZIG download directory /home/m64/ZIG/_downloads ...
```

- Download or move your zig versions all into the directory `~ZIG/_downloads`.
You can leave the tarballs in the _downloads folder, they will not disturb. For example, my directory looks like this:
```
❯ ls -pd ZIG/_downloads/*
ZIG/_downloads/zig-linux-x86_64-0.11.0/
ZIG/_downloads/zig-linux-x86_64-0.11.0.tar.xz
ZIG/_downloads/zig-linux-x86_64-0.12.0/
ZIG/_downloads/zig-linux-x86_64-0.12.0.tar.xz
ZIG/_downloads/zig-linux-x86_64-0.12.0-dev.2536+788a0409a/
ZIG/_downloads/zig-linux-x86_64-0.14.0-dev.2+0884a4341/
ZIG/_downloads/zig-linux-x86_64-0.14.0-dev.2+0884a4341.tar.xz
```
- Any new / old zig version you want to try -> just download the tarball and place it into your `ZIG/_downloads` folder, and extract it there.

## Listing installed- / Switching Versions
- run `zig-select` w/o a parameter: it will list your downloaded directories/zig-versions.
```
./zig-select
Versions available:

zig-linux-x86_64-0.12.0
zig-linux-x86_64-0.12.0-dev.2536+788a0409a
zig-linux-x86_64-0.11.0
zig-linux-x86_64-0.14.0-dev.2+0884a4341

Run this utility again with the corresponding version as argument
```
- run `zig-select zig-linux-x86_64-0.12.0` to switch to it.

