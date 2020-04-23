# dropWPBT

Disables [WPBT table](https://download.microsoft.com/download/8/A/2/8A2FB72D-9B96-4E2D-A559-4A27CF905A80/windows-platform-binary-table.docx) in your firmware.

## Usage

### Requirements

* UEFI-enabled firmware
* Disabled Secure Boot (or sign it yourself)

### Installation

Put `DRIPSEnabler.efi` to a location where it will be executed before Windows starts. If you are using rEFInd, put it under `ESP:\EFI\refind\drivers_x64`. You can also load it using UEFI shell's `startup.nsh`.

Now reboot.
