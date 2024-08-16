# Yocto Kirkstone Instruction for the IASO-W07A-RK3568MB-ABM

![](https://img.shields.io/badge/Release-v4.0-green.svg)
![](https://img.shields.io/badge/License-GPL3.0-orange.svg)



****
## Environment setup and compiling

Please follow this chapter to setup an Yocto compile environment first, then step by step to compile flashable image.

### Step 1
There are two different methods you can use to set up the build environment. One is to install the required packages onto your host filesystem. 
Another is to use a docker container, where the installation of the required packages is automated for you.

General Packages Installation (Ubuntu 20.04 is recommended version for host environment)

    $ sudo apt-get install gawk wget git git-core diffstat unzip texinfo gcc-multilib build-essential \
    chrpath socat cpio python python3 python3-pip python3-pexpect \
    python3-git python3-jinja2 libegl1-mesa pylint3 rsync bc bison \
    xz-utils debianutils iputils-ping libsdl1.2-dev xterm \
    language-pack-en coreutils texi2html file docbook-utils \
    python-pysqlite2 help2man desktop-file-utils \
    libgl1-mesa-dev libglu1-mesa-dev mercurial autoconf automake \
    groff curl lzop asciidoc u-boot-tools libreoffice-writer \
    sshpass ssh-askpass zip xz-utils zstd liblz4-tool kpartx vim screen

Or adapt Docker Container based compile environment (Optional)

    $ sudo docker run --privileged=true --name rk3568_build  -v /home/<user name>/<source folder>:/home/mnt -t -i onlywig/build_rk356x_yocto bash
    (first time)

    $ sudo docker ps -a
    $ sudo docker start <your container id>
    $ docker exec -it rk3568_build bash (after first time)

### Step 2

Source the compile relative commands:

    For IASO-W07A-RK3568MB-ABM
    $ MACHINE=iaso-rk3568-abm DISTRO=abm-qtwayland source iei-rk-setup-release.sh

For a full build:

    $ bitbake core-image-weston

For clean the output image relate files:

    $ bitbake -c clean core-image-weston

For clean the output image with downloaded files:

    $ bitbake -c cleanall core-image-weston


****
## Flashing images

### Step 1
Go to image folder after compiled as last chapter.

    $ cd <source folder>/build/tmp/deploy/images/iaso-rk3568-abm/
    $ ls core-image-weston-iaso-rk3568-abm.update.img (This is flashable compiled image)

### Step 2
Copy image to Windows PC, adapt "RK3568 Basic Operations" document which IEI sent, and flash the image.
  
### Step 3
After flashing, first boot will do hardware configuration such as eMMC storage expansion, then reboot again, it's normal.

### Step 4
Boot into login prompt, and enjoy!

****
