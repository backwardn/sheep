# Linux installation

## Bootloaders

### Supported bootloaders

GRUB is the only one supported bootloader at this time. There is currently no plan to support
more bootloaders.

### Supported boot modes

Sheep is able to install the operating system using either UEFI mode and Legacy (MBR) mode

### Configuration

Configure the bootloader of the future linux OS

* `image` : Path to grub-efi.tar.gz archive - For **UEFI** system only
* `change_boot_order` : **none** (EFI boot entry created but boot order unchanged), **persistent** (change boot order, default) or **once** (change next boot for one reboot only) - Set new EFI menu entry as first in boot order - For **UEFI** system only
* `kernel_parameter` : Kernel parameters you want to add to customize the way your system boots

```yaml
bootloader:
  image: http://path/to/grub-efi.tar.gz
  change_boot_order: none
  kernel_parameter: 'console=ttyS1,57600n8'

```

!!! Note
    Sheep does not support multiboot. Be careful, installating Linux with Sheep on a drive,
    flush the whole partition table on the drive.

## Linux system

Configure your linux OS

* `image` : Path to the linux filesystem image you want to use
* `label` : Name your distribution for **EFI menu entry** and **grub menu** - Default value **Linux**
* `device` : Storage device to contain OS - First storage disk listed during the installation by default
* `rootfsType` : **ext4** & **btrfs** supported - Default value **ext4**
* `rootfsLabel` : label of root partition   
 It has to be 12 characters or less : `[0-9]`  `[a-z]` `[A-Z]` `-`  `_` allowed   
 Default value **rootfs**
* `selinux` : **enable** or **disable** - Default value **disable**
* `blacklist_module` : List kernel module that has to be disable

```yaml
linux:
  image: https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-disk1.img
  label: ubuntu_16_09
  device: /dev/sda
  rootfsType: ext4
  rootfsLabel: cloudimg-rootfs
  selinux: disable
  blacklist_module:
    - mei
    - mei_me

```

!!! Note

    - SELINUX isn't used by every linux distribtuion. For example enabling it for ubuntu will have no effect
    - Permissive mode of Selinux not available for the moment with sheep

## Pxe-pilot

Configure pxe-pilot with sheep installation

* `enable` : **true** or **false**
* `url` : Pxe-pilot API endpoint URL
* `config_after_reboot` : Pxe-pilot configuration name to indicate the machine to reboot on it's hard disk

```yaml
pxePilot:
  enable: true
  url: http://pxe_pilot_server_address
  config_after_reboot: local

```

## Sheep execution

Configure machine reboot by the end of sheep execution.

* `reboot`: **true** or **false**

```yaml
sheep:
  reboot: false
```
