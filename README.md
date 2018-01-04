# meltdownspectre-patches
Summary of the patch status for Meltdown / Spectre

What?
=====

Meltdown and Spectre are hardware design vulnerabilities in all modern CPUs based on
speculative execution. Background infos:

 * https://spectreattack.com/ or https://meltdownattack.com/ (both pages serve identical content)
 * https://googleprojectzero.blogspot.dk/2018/01/reading-privileged-memory-with-side.html

The bug is in the hardware, but mitigations in operating systems are possible and are getting
shipped now. I'm collecting notes on the patch status in various software products. This will
change rapidly and may contain errors. If you have better info please send pull requests.

Linux upstream kernel
=====================

[Kernel Page Table Isolation](https://en.wikipedia.org/wiki/Kernel_page-table_isolation#cite_note-:2-4)
is a mitigation in the Linux Kernel, originally named KAISER.

 * [Version 4.14](https://cdn.kernel.org/pub/linux/kernel/v4.x/ChangeLog-4.14.11) contains KPTI.
 * [Version 4.15-rc6](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/log/?h=v4.15-rc6) contains KPTI.
 * The patches have not been backported to the longterm kernels like 4.9 (state: 4.9.74).

minipli patches
===============

minipli is an unofficial fork of the former grsecurity patches (original grsecurity is no longer publicly
available). minipli is based on the longterm kernel 4.9 which does not contain KPTI yet.

 * [bug report with discussion about backporting KPTI](https://github.com/minipli/linux-unofficial_grsec/issues/25)

Android
=======

 * Fixed with [https://source.android.com/security/bulletin/2018-01-01](Android Security Bulletin—January 2018).

Windows
=======

 * [KB4056892](https://support.microsoft.com/en-us/help/4056892/windows-10-update-kb4056892) is said to fix this based on [this](http://mashable.com/2018/01/03/microsoft-patch-processor-vulnerability/?utm_cid=mash-com-Tw-main-link#NYuDOh55Kqqo) article, but unclear.

OS X
====

 * Unclear, [some Info](https://twitter.com/aionescu/status/948610973987831809).

Linux distributions
===================

 * [Red Hat Advisory](https://access.redhat.com/security/vulnerabilities/speculativeexecution)
 * Ubuntu - nothing yet, https://people.canonical.com/~ubuntu-security/cve/2017/CVE-2017-5754.html
 * Debian - nothing yet, https://security-tracker.debian.org/tracker/CVE-2017-5754

Virtualization
==============

* [XSA-254](https://xenbits.xen.org/xsa/advisory-254.html), no patches yet
* QEMU - nothing yet, discussion: https://lists.nongnu.org/archive/html/qemu-devel/2018-01/msg00613.html

Browsers
========

* Mozilla: [Mitigations landing for new class of timing attack](https://blog.mozilla.org/security/2018/01/03/mitigations-landing-new-class-timing-attack/)
* Chrome: [Actions Required to Mitigate Speculative Side-Channel Attack Techniques](https://www.chromium.org/Home/chromium-security/ssca)
