<!--- @file
  general-guidelines-for-secure-code-review.md for EDK II Secure Code Review Guide

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
# General Guidelines for Secure Code Review {#general-guidelines-for-secure-code-review}

**Overview**

Secure Code Review is a special activity compared to a normal code review. While the typical code review is focused on software quality, including usability, reusability, and maintainability, secure code reviews are focused on software security aspects, including but not limited to confidentiality, integrity, and availability (C.I.A.).

In 2006, Howard from Microsoft, published “A Process for Performing Security Code Reviews.”. It provides some general guidelines for performing a security code review. The guidelines are still valid today:

1.  Make sure you know what you are doing
2.  Prioritize
3.  Review the code.

#### Make sure you know what you are doing {#make-sure-you-know-what-you-are-doing}

Before you review code, please make sure you understand the following:

1.  Threat Model and Security Architecture of the feature, including assets, security objectives, adversaries, and the mitigations.
2.  The general secure design and coding principles for EDK II.

#### Prioritize {#prioritize}

According to “A Process for Performing Security Code Reviews.”, the priority of common software code is below:

1.  Old code
2.  Code that runs by default
3.  Code that runs in an elevated context
4.  Anonymously accessible code
5.  Code listening on a globally accessible network interface
6.  Code is written in C/C++/assembly language
7.  Code with a history of vulnerabilities
8.  Code that handles sensitive data
9.  Complex code
10.  Code that changes frequently

Except for items #4 and #5, all other rules apply to EDK II firmware.

#### Review the code {#review-the-code}

Reviewing the code involves three steps:

1.  Rerun all available code-analysis tools.
2.  Look for common vulnerability patterns, such as
    1.  Integer arithmetic vulnerabilities
    2.  Buffer-overrun vulnerabilities
    3.  Cryptographic vulnerabilities
    4.  Structured Query Language (SQL) Injection vulnerabilities
    5.  Cross-site scripting vulnerabilities
3.  Dig deep into risky code, such as
    1.  Are there logic or off-by-one errors (for example, ‘&gt;’ vs. ‘&gt;=’ or ‘||’ vs. ‘&amp;&amp;’)?
    2.  Is the data correctly validated?
    3.  Are buffer lengths constrained correctly?
    4.  Are integer values range-checked correctly?
    5.  Are pointers validated?
    6.  Can the code become inefficient (for example, O(N<sup>2</sup>)) due to some malformed data (for example, a hash table look-up becomes a list look-up)?
    7.  Are errors handled correctly?

Other than #2.iv and #2.v above, all other rules apply to EDK II firmware.

Besides “A Process for Performing Security Code Reviews.”, Ransome provided some good suggestions in the book “Core Software Security: Security at the Source” on how to perform the SDL activity including security code review.

#### EDK II Secure Coding Guidelines {#edk-ii-secure-coding-guidelines}

We also provided the guideline for EDK II Secure Coding. People need to fully understand the EDK II secure coding best practices before doing the security code review.