# dropWPBT

Disables the WPBT in your firmware. This program use a non-permenant, non-destructive method to remove the table from system memory, so it should be executed every time the computer is rebooted before Windows bootloader starts.

## Usage

### Requirements

* amd64 architecture
* UEFI firmware
* disabled Secure Boot (or sign it yourself)

### Installation

#### With a 3rd party bootloader

Put `dropWPBT.efi` to a location where it will be executed every time before Windows starts.

* [rEFInd](https://www.rodsbooks.com/refind/): `ESP:\EFI\refind\drivers_x64`
* [OpenCore](https://github.com/acidanthera/OpenCorePkg): `ESP:\EFI\OC\Drivers`
* [Clover](https://github.com/CloverHackyColor/CloverBootloader): `ESP:\EFI\CLOVER\drivers\UEFI`

You can also load it using UEFI shell's `startup.nsh`, or even manually.

#### Without an external bootloader

This method is for advanced users. You need to be familiar with how UEFI works. The commands below is just for reference, do not blindly copy and paste!

`dropWPBT-loader.efi` can act as a bootloader itself. To install, launch a `cmd.exe` with Administrator privilege and type something like this:

```
mountvol T: /S
mkdir T:\EFI\boot
cp dropWPBT-loader.efi T:\EFI\boot\bootx64.efi
bcdedit /set {bootmgr} path \EFI\boot\bootx64.efi
mountvol T: /D
```

## FAQ

### What is WPBT?

[WPBT](https://download.microsoft.com/download/8/A/2/8A2FB72D-9B96-4E2D-A559-4A27CF905A80/windows-platform-binary-table.docx) is an ACPI table in your firmware allowing your computer vendor to run a program every time Windows (8 or later) boots. This is a convenient method for computer vendors to force the installation of a service program or an anti-theft software, but this also means your fresh installed Windows will have potentially unwanted 3rd party programs running straight on the first boot, and the end user would have basically no control over it. Also, firmware is not updated as frequently as your OS or everyday software, which means if there is a security vulnerability in the WPBT-loaded program, a fair number of users might never get the update.

A lot PC vendors ([Lenovo](https://borncity.com/win/2017/12/06/vendors-rootkit-windows-platform-binary-table-wpbt/), [ASUS](https://www.dpreview.com/forums/thread/4438288), etc.) are known to utilize WPBT table to run their own programs on the consumer's computer.

### How to verify if my computer have the WPBT table?

You can use one of the following software:

* NirSoft's [FirmwareTablesView](https://www.nirsoft.net/utils/firmware_tables_view.html)
* [RWEverything](http://rweverything.com/)

Note that they might not work if you enabled [HVCI](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/enable-virtualization-based-protection-of-code-integrity).

### How do I know if my OS is already tainted?

Search for `C:\Windows\system32\wpbbin.exe`. Note this program might delete itself after running so this is not a reliable evidence.

### What will happen if I forget to run `dropWPBT.efi` once?

The program inside the WPBT table runs, which typically means your Windows installation is tainted.

### Is there any alternative methods to disable the WPBT?

Hackintosh-oriented bootloaders such as OpenCore have their own config for deleting ACPI tables. Please see their documentation. 

### Is there is a permenant method to remove the WPBT from my firmware?

Some vendors provide an option to disable WPBT on some models. 

* Lenovo: [Lenovo LSE Windows Disabler Tool](https://support.lenovo.com/no/zh/downloads/ds104370)
* ASUS: Disable "ASUS Grid Install Service"

The only permenant method known to me is to modify your motherboard's UEFI firmware. The method is different for every motherboard; you need to have a dump of the UEFI firmware and need to bypass some limitations. I won't stop you from doing that, but keep in mind that you might destory your computer on the way and you will be the only one responsible for it.
