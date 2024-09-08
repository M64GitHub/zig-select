# zig-select
zig-select is a lightweight version management utility designed to efficiently handle multiple ZIG installations within your home directory. With a focus on simplicity, it ensures your ZIG installations are organized and provides a fast, intuitive way to switch between them.

## About

zig-select is a small utility written in bash to easily switch between different versions of zig. 
It should work on any GNU/linux or compatible system (not yet verified on MAC/OSX).
I wrote this utility mainly for myself, please see the gist [Managing multiple versions of ZIG on your system easily](https://gist.github.com/M64GitHub/6d2e0cedb69edd9041c92e1422d9f6b6) to find out more to why and how the
following prerequisites/directories and modus operandus were chosen.  

The script will expect and handle your extracted binary downloads of the zig language in your HOME/ZIG folder.
In order to achieve flexibility, it works with directory names, at least for now:


## Installation / System Setup
- Run the script a first time to create the directories for you:
```
❯ ./zig-select
Creating ZIG root directory /home/m64/ZIG ...
Creating ZIG download directory /home/m64/ZIG/_downloads ...
```
(It is a good idea to store the script in your ~/ZIG folder then. You can copy it to ~/ZIG)

- ADD to your PATH variable: `~/ZIG:~/ZIG/current`.  

ZSH users:
```
echo 'export PATH=$PATH:~/ZIG:~/ZIG/current' >> ~/.zshrc
```
BASH Users:
```
echo 'export PATH=$PATH:~/ZIG:~/ZIG/current' >> ~/.bashrc
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


## Usage
### List installed versions
run `zig-select` w/o a parameter: it will list your downloaded directories/zig-versions.
```
~/ZIG ❯ zig-select
Versions available:

zig-linux-x86_64-0.12.0
zig-linux-x86_64-0.12.0-dev.2536+788a0409a
zig-linux-x86_64-0.11.0
zig-linux-x86_64-0.14.0-dev.2+0884a4341

Run this utility again with the corresponding version as argument
to switch version.
```

### Switch version
run `zig-select version` 
```
zig-select zig-linux-x86_64-0.12.0
```
to switch to it.


## How it works:

```bash
# ----------------- the directory structure in ~/ZIG/
#                   (script will create for you, and
#                    "move" the 'current' symlink):
~/ZIG ❯ ls -lp
total 16
lrwxrwxrwx  1 m64 m64   48 Sep  8 20:42 current -> /home/m64/ZIG/_downloads/zig-linux-x86_64-0.11.0/
drwxrwxr-x  6 m64 m64 4096 Sep  8 16:26 _downloads/
-rwxrwxr-x  1 m64 m64 1518 Sep  8 20:38 zig-select

# ----------------- zig versions stored in the _downloads
#                   folder of ~/ZIG
#                   (copy, extract all versions you
#                    want there)
~/ZIG ❯ ls -p _downloads
zig-linux-x86_64-0.11.0/                     zig-linux-x86_64-0.12.0.tar.xz
zig-linux-x86_64-0.11.0.tar.xz               zig-linux-x86_64-0.14.0-dev.2+0884a4341/
zig-linux-x86_64-0.12.0/                     zig-linux-x86_64-0.14.0-dev.2+0884a4341.tar.xz
zig-linux-x86_64-0.12.0-dev.2536+788a0409a/

# ----------------- running script without a parameter: lists versions
~/ZIG ❯ zig-select
Versions available:

zig-linux-x86_64-0.12.0
zig-linux-x86_64-0.12.0-dev.2536+788a0409a
zig-linux-x86_64-0.11.0
zig-linux-x86_64-0.14.0-dev.2+0884a4341

Run this utility again with the corresponding version as argument
to switch version.

# ----------------- or with a version as parameter: switch to the version
~/ZIG ❯ zig-select zig-linux-x86_64-0.12.0
Using version: zig-linux-x86_64-0.12.0
Removing current symlink ...
Creating new symlink ...
done!

~/ZIG ❯ zig version
0.12.0

~/ZIG ❯ ls -al
total 16
drwxrwxr-x  3 m64 m64 4096 Sep  8 20:41 .
drwxr-x--- 51 m64 m64 4096 Sep  8 20:41 ..
lrwxrwxrwx  1 m64 m64   48 Sep  8 20:41 current -> /home/m64/ZIG/_downloads/zig-linux-x86_64-0.12.0
drwxrwxr-x  6 m64 m64 4096 Sep  8 16:26 _downloads
-rwxrwxr-x  1 m64 m64 1518 Sep  8 20:38 zig-select

# ----- version as parameter: switch to another version ...
~/ZIG ❯ zig-select zig-linux-x86_64-0.11.0
Using version: zig-linux-x86_64-0.11.0
Removing current symlink ...
Creating new symlink ...
done!

~/ZIG ❯ ls -al
total 16
drwxrwxr-x  3 m64 m64 4096 Sep  8 20:42 .
drwxr-x--- 51 m64 m64 4096 Sep  8 20:42 ..
lrwxrwxrwx  1 m64 m64   48 Sep  8 20:42 current -> /home/m64/ZIG/_downloads/zig-linux-x86_64-0.11.0
drwxrwxr-x  6 m64 m64 4096 Sep  8 16:26 _downloads
-rwxrwxr-x  1 m64 m64 1518 Sep  8 20:38 zig-select

~/ZIG ❯ zig version
0.11.0
```
