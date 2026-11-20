# AX210 IntelBTPatcher 2.5.3 Build

This build was produced and verified on:

- Intel AX210 Bluetooth, USB `8087:0032`
- macOS Sequoia 15.8.3, build 24H241, x86_64
- Xcode 16.4, build 16F6
- Lilu 1.7.3
- BlueToolFixup 2.7.2
- IntelBluetoothFirmware 2.4.0
- IntelBTPatcher 2.5.3 from this fork at tag `v2.5.3`,
  commit `8190bcc0c3cadebacd7e4ccd876836247f7cd4ce`

The included IntelBTPatcher contains the LE Data Length Change event
injection that clears the `LE_READY_WAIT_FOR_LENGTH` stall described in
OpenIntelWireless issue #514.

## Validation

- USB Bluetooth reports `Built-In = Yes`.
- Bluetooth controller reports `THIRD_PARTY_DONGLE`, firmware
  `v13719 c13719`, and Bluetooth 5.3.
- A BLE keyboard discovered and paired successfully.
- The keyboard reached `LE_READY_IDLE` with encryption enabled.
- A Bluetooth headset connected and produced audio normally.
- Before this patch, the keyboard stopped at `LE_READY_WAIT_FOR_LENGTH`
  and timed out with status 708.

## Artifact

Release asset:

```text
IntelBTPatcher-v2.5.3-Xcode16.4-x86_64.kext.zip
```

IntelBTPatcher executable SHA-256:

```text
D62B1C14205DC83A5A97BB85430A0E4E03EA36E9F3E085CFDC5EFA6F19D1EC2F
```

Only `IntelBTPatcher.kext` is supplied. Do not load this kext together with
the older IntelBTPatcher release. Keep the matching OpenCore configuration,
Lilu, BlueToolFixup, and IntelBluetoothFirmware versions described above.

The event-injection fix is based on an unmerged upstream issue and is provided
as-is. Back up the EFI before replacing a working kext.
