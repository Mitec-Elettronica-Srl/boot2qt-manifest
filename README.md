# boot2qt-manifest

repo manifest to build boot2qt on MITEC devices.

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
