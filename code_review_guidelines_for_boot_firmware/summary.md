<!--- @file
  summary.md for code_review_guidelines_for_boot_firmware for EDK II Secure Code Review Guide

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

## Summary {#summary}

| **Category** | **Review Detail** |
| --- | --- |
| External Input | What is the external input?<br>How is the external input checked?<br>Does the check happen in all possible paths?<br>What is the action if the check failed?<br>If SMM is involved, how does SMI handler do the check for the communication buffer?<br>If a Variable is involved, how is it consumed?<br>Is ASSERT used? |
| Race Condition | What is the critical resource? <br>If SMM is involved, can the BSP and AP access the same resource?<br>Does the trusted region code access resources in the untrusted region?|
| Hardware Input | What is the hardware input?<br>How is the hardware input checked?<br>Does the check happen in all possible paths?<br>If MMIO is involved, how is the MMIO bar checked? |
| Secret Handling | Where is the secret? <br>How is the secret cleared after use?<br>Does the cleanup function clear all secrets in all places, such as stack, heap, global data, communication buffer, ASCII &lt; = &gt; Unicode, Setup Browser, Key buffer?<br>Is the secret saved into a variable?<br>Does the password follow the general rules, such as strong password requirement, retry time, history, etc?<br>What if the user forgets the password?<br>Is the default password/key used?<br>Is the password/key hardcoded?<br>Does the key comparison algorithm compare entire data?<br>Is side channel guidelines followed?|
| Register Lock | What registers need to be locked? <br>When is the register locked?<br>Is the register lock controlled by some policy?<br>Is the register lock controlled by a variable?<br>Is there any way to bypass the lock?<br>Is the register locked in normal boot, S3, S4?<br>Is the register locked in capsule, recovery?<br>Is the register locked in manufacture mode?|
| Secure Configuration | Is a variable used to control the policy?<br>Is a PCD used to control the policy? If so, what is the PCD type?<br>What is the default configuration?<br>What is the behavior in S3, S4, capsule, recovery, manufacture mode or debug mode? |
| Replay/Rollback | Is LSV or SVN used? <br>Where is the LSV or SVN stored?<br>How are timestamps, nonce, or monotonic counters used? |
| Cryptograph | Is a signing verification algorithm used?<br>Is a deprecated algorithm used?<br>Is Cyclic Redundancy Check (CRC) or checksum used?<br>Should the solution use hash or Hashed Message Authentication Code (HMAC)?<br>Should the solution use symmetric encryption or asymmetric encryption?<br>When is the key deployed and destroyed?<br>Where is the key located?<br>How is the key protected?<br>Is the key root key or session key used to encrypt the data? |









<br>



