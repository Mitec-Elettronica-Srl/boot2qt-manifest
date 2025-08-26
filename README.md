# boot2qt-manifest

repo manifest to build boot2qt on MITEC devices.


## Environment

Refer to yocto [documentation](https://docs.yoctoproject.org/2.0/yocto-project-qs/yocto-project-qs.html) to check what it is to be installed on the compiling system.

Builds are tested in one of these systems:
  - ubuntu 24.04
  - debian 12

Start by installing the repo tool:

```sh
mkdir ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

# add this to .bashrc or .zshrc bepending on the shell you are using
export PATH="~/bin:$PATH"
```

On ubuntu and debian-based distributions install the following:

```sh
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat libsdl1.2-dev xterm file git git-lfs nano libxkbcommon-tools libclang-dev
```

And then also (verified on debian 12):

```sh
sudo apt-get install build-essential chrpath cpio debianutils diffstat file gawk gcc git iputils-ping libacl1 liblz4-tool locales python3 python3-git python3-jinja2 python3-pexpect python3-pip python3-subunit socat texinfo unzip wget xz-utils zstd
```

## Python 2.7 (not needed anymore)

If you enable certain browsers to be compiled you will have to install python2.7 and symlink python executable to python3: you can clone this repo (you will also find it on .repo folder after init):

```sh
cd python2.7
sudo dpkg -i *.deb
```


## How To

First of all create a new directoy to hold sources and compilation results:
```sh
mkdir b2qt_mitec
cd b2qt_mitec
```

Then download sources using the repo tool (the same one used to fetch android):

```sh
repo init -u  https://github.com/Mitec-Elettronica-Srl/boot2qt-manifest.git -m scarthgap.xml
repo sync -j$(nproc)
```

Then set the MACHINE environment variable and source the environment.

Machine is one of the build-machine directory, without build- appendend, for example:

```sh
export MACHINE=imx8mm-var-dart
source ./setup-environment.sh
```

Then you can proceed at building targets:

```sh
bitbake <target>
```

## Tips and Tricks

When building in a machine with a large number of cores (like 28 or higher) and not much RAM do the following to limit resources usage:
```sh
export BB_NUMBER_THREADS="6"
export PARALLEL_MAKE="-j6"
```

These must be done before sourcing setup-environment.sh

__WARNING__: Doing an unrestricted build will easily occupy more than 60GB of swap.

## Supported Devices

The following is a list of supported devices (MACHINE names):
  - imx8mm-var-dart
