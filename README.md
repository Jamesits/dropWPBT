# dropWPBT

Disables the WPBT table in your firmware.

## Usage

### Requirements

* UEFI-enabled firmware
* Disabled Secure Boot (or sign it yourself)

### Installation

Put `dropWPBT.efi` to a location where it will be executed every time before Windows starts. If you are using rEFInd, put it under `ESP:\EFI\refind\drivers_x64`. You can also load it using UEFI shell's `startup.nsh`.

## FAQ

### What is WPBT?

[WPBT table](https://download.microsoft.com/download/8/A/2/8A2FB72D-9B96-4E2D-A559-4A27CF905A80/windows-platform-binary-table.docx) is an ACPI table in your firmware allowing your computer vendor to run a program every time Windows (8.1 or later) boots. This is a convenient method for computer vendors to force the installation of a service program or an anti-theft software, but this also means your fresh installed Windows will have potentially unwanted 3rd party programs running straight on the first boot, and the end user would have basically no control over it. Also, firmware is not updated as frequently as your OS or everyday software, which means if there is a security vulnerability in the WPBT-loaded program, a fair number of users might never get the update.

A lot PC vendors ([Lenovo](https://borncity.com/win/2017/12/06/vendors-rootkit-windows-platform-binary-table-wpbt/), [ASUS](https://www.dpreview.com/forums/thread/4438288), etc.) are known to utilize WPBT table to run their own programs on the consumer's computer.

### How to verify if my computer have the WPBT table?

You can use one of the following software:

* NirSoft's [FirmwareTablesView](https://www.nirsoft.net/utils/firmware_tables_view.html)
* [RWEverything](http://rweverything.com/)

Note that they might not work if you enabled [HVCI](https://docs.microsoft.com/en-us/windows/security/threat-protection/device-guard/enable-virtualization-based-protection-of-code-integrity).
