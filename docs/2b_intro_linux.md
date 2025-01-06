# Practical 2 Pre-Setup: Ubuntu Installation and Brief Intro to Linux 

[TOC]

## Linux Installation 

From this point on, this course will be primarily using the Ubuntu 22.04 Operating System. This is primarily because the majority of robotics and aerial robotics development activities in research and industry are developed for use on Linux-based systems (of which Ubuntu is one). In particular we will be primarily using ROS2 and ROS2 derived tools, which currently works best within Ubuntu 22.04. 

We’ve explored alternatives like Windows and MacOS (including both Intel and Apple Silicon/M1/2 versions) in previous course iterations. Unfortunately, these platforms introduced significant challenges, including:

  - Compatibility issues with ROS2 and its dependencies.
  - Variability in performance and tool availability.
  - Increased troubleshooting effort for both students and instructors.

Ultimately reducing the quality of the course. Therefore this course would like to focus on providing the greatest course quality by focussing on Ubuntu. 

While containers (e.g., Docker) and virtual machines (VMs) can offer flexibility, they have limitations in this context:

  - *Docker*: Known for portability, but graphical user interfaces (GUIs) for simulation tools like Gazebo and RViz can be challenging to configure, especially on Windows.
  - *Virtual Machines*: Simulations in Gazebo are graphics-intensive, and VMs often lack the hardware acceleration needed for smooth operation. Additionally, VMs can have limited access to host machine IO interfaces (e.g., USB), making hardware integration difficult.

That said, students are welcome to experiment with Docker or VMs, but these methods will receive minimal support from the course instructors.

In order to enable as many of the students to work on native Ubuntu as possible, we suggest the following options:

1. Dual Booting your Windows Install with Ubuntu 22.04
    - Install Ubuntu 22.04 alongside your existing Windows installation. This allows you to choose between operating systems at boot.
    - Native ubuntu performance
    - Fully supported by course instructors 
    - Will require at least 100Gb of unused disk space
    - Windows only
2. Borrowing and booting from an Ubuntu 22.04 installed USB-C NVME Drive 
    - Borrow or prepare a portable USB-C NVMe drive pre-installed with Ubuntu 22.04. This method allows you to run Ubuntu without altering your main system.
    - Go to bios setting to reorder your booting.
    - Different brands of computers have different ways of getting into bios. For example, for dell computer, you could access the BIOS/UEFI settings by restarting your computer and pressing the F2 key repeatedly as soon as the Dell logo appears. 
    - Minimal changes to your primary system.
    - Requires a USB-C port with fast read/write capabilities.
    - Limited number of pre-setup Ubuntu 22.04 bootsticks
    - Windows Primarily, but known to potentially work with Mac OSX too (pending testing). 
3. Repurpose an old laptop 
4. Spin up a virtual machine on a cloud provider
    - Use a cloud provider like AWS, Google Cloud, or Azure to spin up a virtual machine running Ubuntu 22.04
5. Docker
    - Docker may be possible for some of the situations
    - Known issues with GUIs and Windows (which can be solved) 
    - Not as supported 
6. Virtual Machine

<!-- ## Installing Ubuntu 22.04

There are three ways you can run this project depending on your situation or operating system. 

- Linux: All 2 ways (Local and Docker) will work
- Windows: Boot from an external SSD provided by us
- Max OSX: TBC

## For Linux users
If you are a Linux user, you will have two options to set up your project, i.e. Local or Docker.

### Local

Install Ubuntu 22.04, ROS2 Humble, Ignition Gazebo Fortress as per their instructions.

#### 1. 

Your options are 

1. Finding a spare machine that you can wipe and install Ubuntu on
2. Finding a machine that you would be willing to dual boot
3. Running a virtual machine
4. Running a container (Not supported yet as I havent made a container - also this requires gazebo which requires a GUI which is not ideal for containers apart from singularity containers) -->

For options 1 and 2, you will need to find a USB stick that is >4Gb and using a tool such as [Rufus](https://rufus.ie/en/) flash the [Ubuntu 22.04 ISO file](https://ubuntu.com/download/desktop) onto it. 

Once you have a flashed USB drive, you can insert that into the spare machine. On startup make sure to mash some combination of F2, F8 or F12 to go to the BIOS boot screen and select boot from USB. 

This will start up tp the Ubuntu installer on the USB drive where you can select what to do. Whether that is to wipe the machine, or in the advanced menu create a new partition for Ubuntu so you can dual boot (For Windows you will also need to shrink your primary partition). For more details [see a guide such as this one](https://www.onlogic.com/company/io-hub/how-to-dual-boot-windows-11-and-linux/). 

We have also created a number of pre-installed NVME drives which you may be able to borrow pending numbers

<!-- You can also download the ISO file and run it in a virtual machine program such as [VirtualBox](https://www.virtualbox.org/). 

> I have created and exported a virtual machine with everything already installed for you to use. Speak to the instructors

In virtualbox you can import an existing virtual machine. Once installed and you have the gui up, there is an option to import (orange arrow), in which you can select the existing exported virtual machine.
Once you have a virtual machine setup, you can simply start it. 

> Note: Since this project uses gazebo and is not the lightest workioad, you may want to give the VM more resources i.e. CPU, RAM and potetially video memory too. You can do this in the virtual machine settings.  -->



## A Brief Introduction to Linux

Adapted from this [digital ocean tutorial](https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-basics)

### What is Linux
Linux is a family of free and open-source operating systems based on the Linux kernel (core operating system). Operating systems based on Linux are known as Linux distributions or distros. Examples include Debian, Ubuntu, Fedora, CentOS, Gentoo, Arch Linux, and many others.

The Linux kernel has been under active development since 1991, and has proven to be extremely versatile and adaptable. You can find computers that run Linux in a wide variety of contexts all over the world, from web servers to cell phones. Today, 90% of all cloud infrastructure and 74% of the world’s smartphones are powered by Linux.

However, newcomers to Linux may find it somewhat difficult to approach, as Linux filesystems have a different structure than those found on Windows or MacOS. Additionally, Linux-based operating systems depend heavily on working with the command line interface, while most personal computers rely on graphical interfaces.

### The Terminal

The terms “terminal,” “shell,” and “command line interface” are often used interchangeably, but there are subtle differences between them:

* A **terminal** is an input and output environment that presents a text-only window running a shell.
* A **shell** is a program that exposes the computer’s operating system to a user or program. In Linux systems, the shell presented in a terminal is a command line interpreter. The default shell in Ubuntu Linux is known as `bash`.
* A **command line interface** is a user interface (managed by a command line interpreter program) which processes commands to a computer program and outputs the results.

When someone refers to one of these three terms in the context of Linux, they generally mean a terminal environment where you can run commands and see the results printed out to the terminal, such as this:

![linux terminal](images/2_linux-terminal-on-ubuntu.png)

There are two ways to open a terminal:

1. Pressing the ++win++ or ++cmd++ key to open the program menu and typing `terminal`, then pressing ++enter++
2. Pressing ++ctrl+alt+t++

This default terminal is known as the 'gnome-terminal'. Other terminals exist such as ['terminator'](https://terminator-gtk3.readthedocs.io/en/latest/)

Becoming a Linux user requires you to be comfortable with using a terminal. Any administrative task, including file manipulation, package installation, and user management, can be accomplished through the terminal. The terminal is interactive: you specify commands to run (after the $ sign) and the terminal outputs the results of those commands. To execute any command, you type it into the prompt and press ++enter++.

When using the Starling system, interacting with Docker and ROS2, you'll most often be doing so through a terminal shell. Although personal computers that run Linux often come with the kind of graphical desktop environment familiar to most computer users, it is often more efficient or practical to perform certain tasks through commands entered into the terminal. As of writing, a GUI (Graphical User Interface) has not been developed for Starling, and so almost all tasks have to be achieved through the terminal shell.

A basic command to try out is `echo`, which will print things to the terminal. For example `echo hello-world` will print `hello-world` into the terminal. You can also use it to observe the value of **Environment Variables** which record and keep useful variables to the operation of the Operating System. For example, when you run a command in `bash`, `bash` will look for the command executable in the locations provided by the environment variable `PATH`. You can print the contents of this env-var using `echo $PATH`. The `$` before the name of the variable tells `bash` that the following word represents an environment variable, and that it should be looked up.

### Navigating the file system

Like Windows and Mac, the Linux filesystems are based on a directory tree. This means that you can create directories (which are functionally identical to folders found in other operating systems) inside other directories, and files can exist in any directory.

The forward slash (`/`) is used to indicate the root directory in the filesystem hierarchy.

When a user logs in to the shell, they are brought to their own user directory, stored within `/home/<username>`. This is referred to as the user’s home directory. Often you may see the *tilde* (`~`) character when specifying a file location (e.g. `~/Documents/hello.txt` = `/home/<username>/Documents/hello.txt`). This is shorthand for the user's home directory and gets substituted in when used.

To see what directory you are currently active in you can run the `pwd` command, which stands for “print working directory”
```console
myuser@my-machine:~$ pwd
/home/myuser
```

To see a list of files and directories that exist in your current working directory, run the `ls` command:
```console
myuser@my-machine:~$ ls
 Desktop                    Documents
 Downloads                  Pictures
 Public                     Wallpapers
```
You can get more details if you run `ls -al` command:

```console
myuser@my-machine:~$ ls -al
drwxr-xr-x  2 myuser myuser   4096 Apr 30  2021  Desktop
drwxrwxr-x  8 myuser myuser   4096 Oct 29 09:27  Documents
drwxrwxr-x  8 myuser myuser   4096 Dec 10 14:41  Downloads
drwxrwxr-x  8 myuser myuser   4096 May 23 10:43  Pictures
drwxrwxr-x  8 myuser myuser   4096 Jan 19  2017  Public
drwxrwxr-x  8 myuser myuser   4096 Oct 15 09:43  Wallpapers
```

You can create one or more new directories within your current working directory with the `mkdir` command, which stands for “make directory”. For example, to create two new directories named testdir1 and testdir2, you might run the first command. You can create nested directories by using the `-p` option:
```console
myuser@my-machine:~$ mkdir testdir1 testdir2
myuser@my-machine:~$ mkdir -p testdir3/testsubdir
```

To navigate into one of these new directories, run the cd command (which stands for “change directory”) and specify the directory’s name:
```console
myuser@my-machine:~$ cd testdir1
myuser@my-machine:~/testdir1$
```

Note that you can navigate from anywhere to anywhere. `cd` only requires a valid filepath. Note also that `.` represents the current folder and `..` represents the parent folder. Note also how is shows the current working directory in the shell as well.
```bash
cd # This will bring you back to home directory
cd testdir3/testsubdir # Brings you into testsubdir
cd ../ # Brings you back out one level into testdir3
cd ../testdir1 # Brings you back out one level and back into testdir1
cd /home/<username>/testdir2 # Absolute reference to testdir2
cd ~/testdir2 # Absolute reference using tilde to testdir2
```

### Working with files

You cannot use cd to interact with files; cd stands for “change directory”, and only allows you to navigate directories. You can, however, create, edit, and view the contents of files.

One way to create a file is with the touch command. This creates an empty file in your current working directory. To create a new file called file.txt:
```bash
touch file.txt
```

If you decide to rename file.txt later on, you can do so with the mv command. mv stands for “move” and it can move a file or directory from one place to another. By specifying the original file, file.txt, you can “move” it to a new location in the current working directory, thereby renaming it.
```bash
mv file.txt newfile.txt
```

It is also possible to copy a file to a new location with the cp command. If we want to copy newfile.txt, you can make a copy of newfile.txt named newfile_copy.txt like this:
```bash
cp newfile.txt newfile_copy.txt
```

However, files are not of much use if they don’t contain anything. To edit files, a file editor is necessary.
There are many options for file editors, all created by professionals for daily use. Such editors include vim, emacs, nano, and pico.
`nano` is a suitable option for beginners: it is relatively user-friendly and doesn’t overload you with cryptic options or commands.
```bash
nano file.txt
```
This will open a space where you can start typing to edit the file. In `nano` specifically you can save your written text by pressing ++ctrl+x++, ++y++, and then ++enter++. This returns you to the shell with a newly saved `file.txt`.

Now that file.txt has some text within it, you can view it using `cat` or `less`.

The `cat` command prints the contents of a specified file to your system’s output. Try running `cat` and pass the `file.txt` file you just edited as an argument:
```bash
cat file.txt
```

Using `cat` to view file contents can be unwieldy and difficult to read if the file is particularly long. As an alternative, you can use the `less` command which will allow you to paginate the output. Use `less` to view the contents of the file.txt file, like this:
```bash
less file.txt
```
This will also print the contents of file.txt, but one terminal page at a time beginning at the start of the file. You can use the spacebar to advance a page, or the arrow keys to go up and down one line at a time. Press ++q++ to quit out of `less`.

Finally, to delete the file.txt file, pass the name of the file as an argument to `rm`:
```bash
rm file.txt
rm -d directory
rmidr directory
rm -r directory # If the directory you are deleting is not empty
```

> **NOTE**: If your question has to do with a specific Linux command, the manual pages offer detailed and insightful documentation for nearly every command. To see the `man` page for any command, pass the command’s name as an argument to the `man` command - `man command`.
> For instance, `man rm` displays the purpose of `rm`, how to use it, what options are available, examples of use, and more useful information.


> **NOTE**: If a command fails or is hanging or you just want to stop it, most of the time you can stop the running process by pressing ++ctrl+c++. This will send a Keyboard Interrupt message to the program and hopefully stop it.

### Installing Dependencies and Useful Programs

Like windows and mac, individual programs can be manually downloaded (usually as a `tar.gz` file instead of `exe`) and manually installed into your operating system (using `dpkg`). However, the linux project offers a much more straight forward method through the `apt` (Advanced Packaging Tool) utility. `apt` is a free-software user interface that works with core libraries to handle the installation and removal of software on Debian operating systems like Ubuntu. (For other distributions you may come across equivalents like `yum`). This is the primary method for installing software onto your system.

To use `apt`, and more specifically `apt-get` which 'gets' programs for you, you must first run the `update` command to get the current list of all available software. Note that because `sudo` is used, you will most likely need to input your password. `sudo` will be explained below.
```bash
sudo apt-get update
```
> **Note** that it will hang (stop responding) or fail if you are not connected to the internet.

#### Installing Git and VSCode

You can then install your programs using `apt-get install`. For Starling, you will need to use the `git` version control software to both download Starling and eventually build your own controllers. To install `git`, run the following:
```bash
sudo apt-get install git
```

We also recommend the use of [Visual Studio Code](https://code.visualstudio.com/) as your development environment or text editor, but you are free to use whatever you want (atom, notepad++ etc etc). We heavily make use of it during development and recommend a number of extensions. VScode can be installed using the `snap` utility. `snap` is a slightly more modern successor to `apt` for more general programs. `snap` comes ready installed on your linux distrubtion.
```bash
sudo snap install code --classic
```

#### `sudo`
Now in these commands, we have prefixed all of them with `sudo`. `sudo` these days usually stands for `superuser do` and allows a command to be run with the privileges of the superuser (aka the *root* user), if the user has been given permissions to do so. Any command which installs or modifies directories outside of the users home directory will often need superuser privileges to avoid non-superusers from changing things they shouldn't. As the above commands all seek to install programs to the system, they need superuser permissions to do so. Running without `sudo` will give you a permission error. Running a command with `sudo` will ask you for your *own accounts* password.


#### Installing Docker

For Linux systems, see the following [install page](https://docs.docker.com/engine/install/ubuntu/). There are multiple ways of installation docker, but we recommend installing using the repository method:

1. Update the `apt` repository and install requirements

        sudo apt-get update

        sudo apt-get install \
            apt-transport-https \
            ca-certificates \
            curl \
            gnupg \
            lsb-release

2. Add Docker's official GPG key:

        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

3. Add Docker's repository:

        echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

4. Install Docker (and docker-compose!):

        sudo apt-get update

        sudo apt-get install docker-ce docker-ce-cli docker-compose containerd.io

5. Test Docker installation:

        sudo docker run hello-world

This will install Docker, accessible using `sudo` root privileges only. To use docker without sudo, run the following (there are [security issues](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user) with this, but it doesn't matter for running Starling locally)

1. Run the following

        sudo groupadd docker
        sudo usermod -aG docker $USER

2. Log out and log in again to enforce changes
3. Verify that it was successful (we will come back to this command):

        docker run hello-world

That is Docker on Linux installed. See [the original page](https://docs.docker.com/engine/install/ubuntu/) for any further details.
