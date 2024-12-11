# Overview of Linux
 
**Table of Contens**
- [Linux filesystem and hierarchy](#Linux-filesystem-and-hierarchy)
- [SSH Server Configuration & secure the SSH server](#SSH-Server-Configuration)

## Linux filesystem and hierarchy
- ***Linux filesystem*** : The Linux filesystem is the foundation of any Linux-based operating system. It dictates how files are stored, organized, and accessed. Understanding this system is crucial for any DevOps engineer, as it influences everything from system performance to security and deployment processes. This article aims to provide a comprehensive guide to the Linux filesystem, breaking down its structure, key concepts, and practical applications.

- ***Hierarchy***: The Linux filesystem is hierarchical, meaning it has a root directory (/) from which all other files and directories branch out, forming a tree-like structure. This structure is consistent across all Linux distributions, making it easier to navigate and manage multiple systems. The Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Linux systems. Adherence to FHS ensures that software behaves predictably across different Linux distributions.

 The root directory (/) serves as the starting point of the filesystem. Every single file and directory starts from the root directory. The only root user has the right to write under this directory. 

 ![Screenshot from 12-12-2024 2 10-11-24](https://i.ibb.co.com/ygrpSPF/root.png)

 ![Screenshot from 12-12-2024 2 10-11-24](https://i.ibb.co.com/BnYtZC3/Untitled.png)

 - **/** : The root directory of the entire filesystem hierarchy, everything is nestled under this directory.
 - ***bin*** : contains essential executable files required for basic system functionality, such as command binaries like ls, cp, and mv.
 - ***boot*** : contains Bootloader files, including the kernel and folders such as conf, grub, etc.
 - ***dev*** : Device files representing hardware components.
 - ***etc*** : contains all configure-related files.
 - ***home*** : contains all user profiles. As a user, you’ll put your files, notes, programs, etc., in your home directory.
 - ***root*** : Home directory for the root user.
 - ***sbin*** : Contains essential system binaries, usually can only be run by root.
 - ***tmp*** : Storage for temporary files and the contents of the /tmp directories are deleted when your system restarts. Some Linux systems also delete files old files automatically so do’ store anything important here.
 - ***usr*** : User binaries and program data,
   - ‘/usr/share’ contains documentation or is common to all libraries, for example ‘/usr/share/man’ contains the text of the manpage,
   - ‘/usr/lib’ contains the system libraries,
   - ‘/usr/sbin’ contains additional commands for the administrator
 - ***var*** : contains the variable file that is changed dynamically like database, web server 
 - ***lib*** : It's a Shared libraries and it's basically codes that can be used by the executable binaries.
 - ***media*** : Mount point for removable media. When you connect a removable media such as a USB disk, SD card, or DVD, a directory is automatically created under the /media directory for them. You can access the content of the removable media from this directory.
 - ***mnt*** : it's a mount directory and mnt is used by system administrators to manually mount a filesystem.
 - ***opt*** : optional or third-party software.
 - ***srv*** : It contains server-specific and server-related files. For example, if you run a HTTP server, it’s a good practice to store the website data in the /srv directory.


## SSH Server Configuration & secure the SSH server. 

 
