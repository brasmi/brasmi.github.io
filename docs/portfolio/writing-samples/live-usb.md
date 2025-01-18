# Create a live USB boot drive

## Introduction

This guide outlines the steps for creating a live USB recovery drive. A live USB is handy for troubleshooting your native operating system (OS) install or installing a new OS from scratch. 

### Prerequisites

Before you start, you'll need:

* A USB drive with 4GB of space or more
* An operating system ISO to write to the USB drive. In this guide, we'll be using [Ubuntu 22.04.5 LTS](https://releases.ubuntu.com/22.04/){ .external target="blank" }.
* Software for writing the ISO to the USB drive. I recommend [balenaEtcher](https://etcher.balena.io/) as it supports MacOS, Ubuntu, and Windows. 

## Download the image

Download your desired operating system image. For the purposes of this guide, I'm using [Ubuntu 22.04.5 LTS](https://releases.ubuntu.com/22.04/){ .external target="blank" }.

## Create the live USB drive

After downloading the OS image, write the ISO to a USB drive using [balenaEtcher](https://etcher.balena.io/) to create your installation media. 

1. Select **Flash from file** and choose the ISO you downloaded.

2. Next, **Select target** and identify the USB drive you want to flash the image to then press **Select**. 

3. Once the ISO and installation media have been configured, select **Flash!**.

## Boot from the drive

1. Insert the live USB drive into the system you want to use the recovery OS with and power on or restart your device. 

2. While the system boots up, hold down the F12 key (or the key specific to your motherboard's manufacturer for boot menu access, typically F2, Del, or Esc) to access the boot device selection menu.

3. When prompted, select the **Try Ubuntu without installing** option to boot into the live USB environment. This may take a few minutes.

## References

{Include references and/or links to other related docs, such as other how-to guides, concepts, troubleshooting or support information, and limitation details.

* Reference link

* Concept link

* Troubleshooting link}