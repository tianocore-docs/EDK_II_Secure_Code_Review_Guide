<!--- @file
  register-lock.md for EDK II Secure Code Review Guide

  Copyright (c) 2019, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

-->

## Register Lock {#register-lock}

When the system powers on, most of the silicon registers are unlocked. The firmware code needs to configure the system and lock the critical resources by setting the lock bit in a silicon register. Examples include but are not limited to flash chip lock, SMM lock, SMI lock, MMIO BAR configuration lock, Model Specific Register (MSR) configuration lock, etc.

**Previous Vulnerabilities:**

### Flash {#flash}

In 1998, older platforms did not properly lock access to the flash parts, allowing anyone to overwrite BIOS code. Sixty million computers were believed to be infected by the [CIH](https://en.wikipedia.org/wiki/CIH_(computer_virus)) virus.

In [Power Of Community 2007](http://powerofcommunity.net/poc2007/sunbing.pdf), a new attack appeared which took advantage of the Intel top swap feature, if the latter capability was unlocked.

Today, there are several ways to lock the flash part, and the firmware should lock all the possible ways, in proper time, and in all boot paths. These paths include a normal boot, S3, S4, capsule update, recovery, etc.

### SMRAM {#smram}

It is likely the first documented SMM attack, which occurred because the [SMM memory range was not locked](https://www.researchgate.net/publication/241643659_Using_CPU_System_Management_Mode_to_Circumvent_Operating_System_Security_Functions).

Platforms must lock SMRAM in silicon and setup SMRR for all processors to protect SMRAM. This lock must happen in all boot paths (normal boot, S3, S4, capsule update, recovery, etc.).

### MMIO BAR {#mmio-bar}

In [BlackHat 2008](https://invisiblethingslab.com/resources/bh08/part2-full.pdf), Invisible lab demonstrated how to use unlocked remap registers for SMM or Management Engine (ME) firmware to inject code.

Today, all critical MMIO bars are required to be locked without overlap. The configuration is checked by the ACM during a TXT DRTM launch.