---
description: Things i discover while studying Embedded Android
---

# Linux

The init process, which initiates the kernel of our computer  . Init is the first process to be ran by the computer \(since it starts until it shuts off, so its PID is 1\), as we've seen, there are three possibilities of init programs on the linux systems: SystemV, systemd and Upstart, if you check them on the respective folders you're probably gonna find all of them because Ubuntu for instance, keeps all of them to maintain the retrocompatibility.

 

`$ sudo stat /proc/1/exe`

`File: /proc/1/exe -> /lib/systemd/systemd`

