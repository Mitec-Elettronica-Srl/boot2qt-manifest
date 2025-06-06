# boot2qt-manifest

repo manifest to build boot2qt on MITEC devices.


## Environment

Refer to yocto [documentation](https://docs.yoctoproject.org/2.0/yocto-project-qs/yocto-project-qs.html) to check what it is to be installed on the compiling system.

Builds are tested in one of these systems:
  - ubuntu 24.04
  - debian 12

Start by installing the repo tool:

```sh
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo

# add this to .bashrc or .zshrc bepending on the shell you are using
export PATH="~/bin:$PATH"
```

On ubuntu and debian-based distributions install the following:

```sh
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat libsdl1.2-dev xterm file git git-lfs nano
```

Also remember to install python2.7 and symlink python executable to python3.


## How To

First download sources using the repo tool (the same one used to fetch android):

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


## Supported Devices

The following is a list of supported devices (MACHINE names):
  - imx8mm-var-dart
