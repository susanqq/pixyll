---
layout:     post
title:      How to mount remote folder over ssh on mac
date:       2017-09-06
summary:    This is a turtorial on how to mount remote folder for mac system
categories: jekyll pixyll
---
## Install brew if not installed
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
## Install FUSE and SSHFS

### Install FUSE
```
brew cask install osxfuse
```
or download through the link: [fuse](https://github.com/osxfuse/osxfuse/releases/download/osxfuse-3.6.3/osxfuse-3.6.3.dmg)
### Install SSHFS
```
brew install sshfs
```
Or download sshfs here: [sshfs](https://github.com/osxfuse/sshfs/releases/download/osxfuse-sshfs-2.5.0/sshfs-2.5.0.pkg)
For other operation systems, check the link here:
[link](https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh)

### SSh to your server
```
sudo sshfs -o allow_other,defer_permissions,IdentityFile=~/.ssh/id_rsa user@host:/remotefolder/ /localfolder
```

Then your remote folder will appear in your local address.
#### Common Issues:
If you end up with error message:
 ```
 mount_osxfuse: mount point localfolder is itself on a OSXFUSE volume
 ```
You can check whether it is already mounted by do
```
 mount
```

If you get the message like the following:
```
/dev/disk1 on / (hfs, local, journaled)
devfs on /dev (devfs, local, nobrowse)
map -hosts on /net (autofs, nosuid, automounted, nobrowse)
map auto_home on /home (autofs, automounted, nobrowse)
/dev/disk2 on /Volumes/FUSE for macOS (hfs, local, nodev, nosuid, read-only, noowners, quarantine, mounted by yang)
user@host:/remotefolder/ on /localfolder (osxfuse, synchronous)
```
Then you can simply "umount" it to fix this issue.
```
umount user@host:/remotefolder/
```

If you cannot umount or mount an sshfs volume after ssh:
```
pgrep -lf sshfs
```

```
kill -9 <pid_of_sshfs_process>
```

```
sudo umount -f <mounted_dir>
```