---
description: Things i discover while studying Embedded Android
---

# Linux

The init process, which initiates the kernel of our computer and is a parent daemon process of all other processes in linux is the first process to be ran by the computer \(since it starts until it shuts off, so its PID is 1\), as we've seen, there are three possibilities of init programs on the linux systems: SystemV, systemd and Upstart, if you check them on the respective folders you're probably gonna find all of them because Ubuntu for instance, keeps all of them to maintain the retrocompatibility.

Location of the init programs:

`/usr/lib/systemd`

`/usr/share/upstart`

`/etc/init.d`

 To check which one your system uses:

`$ sudo stat /proc/1/exe`

`File: /proc/1/exe -> /lib/systemd/systemd`

In this case, systemd. Some say that systemd is the future for some reason. In fact this command was issued on an Ubuntu 18.04. The reason why one can stumble with this matter is because from Ubuntu 16.04 to 18.04 the location of etc/init.d/rc changes because of systemd.



