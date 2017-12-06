# [QEMU](https://www.qemu.org/)

Notes on QEMU, the open source machine emulator and virtualiser.

* [QEMU Wiki](https://wiki.qemu.org/Main_Page)
* [QEMU User Wiki](https://wiki.qemu.org/Category:User_documentation)
* [QEMU Developer Wiki](https://wiki.qemu.org/Category:Developer_documentation)
* [QEMU User Manual](https://qemu.weilnetz.de/doc/qemu-doc.html#Introduction), also called User Documentation.

## Basic Steps to setup a Live OS with Port Forwarding

```bash
qemu-system-x86_64 -m 512 -net user,hostfwd=tcp::10000-:10000 -cdrom alpine-standard-3.7.0-x86_64.iso
```

## QEMU Manual

## 1 Introduction

QEMU is a FAST! processor emulator using dynamic translation to achieve good emulation speed. QEMU has two operating modes:

* Full system emulation - virtualisation
* User mode emulation - emulation (?), similar to Wine?

## 2 QEMU PC System emulator

### 2.1 [Introduction](https://qemu.weilnetz.de/doc/qemu-doc.html#pcsys_005fintroduction)

Support, features, etc - see online manual.

### 2.2 Quick Start