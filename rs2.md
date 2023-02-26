# RealSense Packages and Libraries Installation

Register the server's public key:

```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE
```

Add the server to the list of repositories:

```shell
sudo add-apt-repository "deb https://librealsense.intel.com/Debian/apt-repo $(lsb_release -cs) main" -u
```

Install the libraries (see section below if upgrading packages):

```shell
sudo apt-get install librealsense2-dkms
sudo apt-get install librealsense2-utils
```

The above two lines will deploy librealsense2 udev rules, build and activate kernel modules, runtime library and executable demos and tools.

Lastly, install the developer and debug packages:

```shell
sudo apt-get install librealsense2-dev
```