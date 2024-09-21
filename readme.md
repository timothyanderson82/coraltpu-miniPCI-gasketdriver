# Introduction
This is a guide to get the Coral EdgeTPU miniPCI version working on Ubuntu 22.04.1 LTS. This compiles various sources of information into a single guide to be consumed by anyone facing the same problems i did.

# References
Issue on Coral Github: https://github.com/google-coral/edgetpu/issues/695
Steps on building the Gasket Driver from the repo: https://github.com/google-coral/edgetpu/issues/808#issuecomment-1909019568
Installing dh-dkms: https://github.com/google-coral/edgetpu/issues/808#issuecomment-1825849055
Original install docs: https://coral.ai/docs/m2/get-started/#2a-on-linux
gasket-driver: https://github.com/google/gasket-driver

# Steps

Follow these steps to build and install the latest gasket-driver:

1. install the required prereqs:
```bash
sudo apt update
sudo apt upgrade
sudo apt install devscripts debhelper dh-dkms -y
```
2. Clone the Repo:
```bash
git clone https://github.com/google/gasket-driver.git
```
3. build the driver:
```bash
cd gasket-driver; debuild -us -uc -tc -b; cd ..
```
4. Verify that it built:
```bash
ls -l gasket-dkms*
```
4. Install the Driver:
```bash
sudo dpkg -i gasket-dkms_1.0-18_all.deb
```
5. Select the driver:
```bash
sudo modprobe apex
```
6. check it worked:
```bash
lsmod | grep apex
```

