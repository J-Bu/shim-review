This repo is for review of requests for signing shim.  To create a request for review:

- clone this repo
- edit the template below
- add the shim.efi to be signed
- add build logs
- add any additional binaries/certificates/hashes that may be needed
- commit all of that
- tag it with a tag of the form "myorg-shim-arch-YYYYMMDD"
- push that to github
- file an issue at https://github.com/rhboot/shim-review/issues with a link to your branch
- approval is ready when you have accepted tag

Note that we really only have experience with using grub2 on Linux, so asking
us to endorse anything else for signing is going to require some convincing on
your part.

Here's the template:

-------------------------------------------------------------------------------
What organization or people are asking to have this signed:
-------------------------------------------------------------------------------
Unicon Software Entwicklungs- und Vertriebsgesellschaft mbH

-------------------------------------------------------------------------------
What product or service is this for:
-------------------------------------------------------------------------------
eLux® is a hardware-independent operating system for cloud computing environments

-------------------------------------------------------------------------------
What's the justification that this really does need to be signed for the whole world to be able to boot it:
-------------------------------------------------------------------------------
We plan to support secure boot with our next release of eLux RP6 having a signed shim
will allow us to be hardware independant.

-------------------------------------------------------------------------------
Who is the primary contact for security updates, etc.
-------------------------------------------------------------------------------
- Name: Niels Keunecke
- Position: Managing Director
- Email address: niels.keunecke@unicon-software.com
- PGP key, signed by the other security contacts, and preferably also with signatures that are reasonably well known in the linux community: N/A
- s/mime certificate: nkeunecke.cer

-------------------------------------------------------------------------------
Who is the secondary contact for security updates, etc.
-------------------------------------------------------------------------------
- Name: Muhammed-Ali Findik
- Position: CDO
- Email address: muhammed-ali.findik@unicon-software.com
- PGP key, signed by the other security contacts, and preferably also with signatures that are reasonably well known in the linux community: N/A
- s/mime certificate: mfindik.cer

-------------------------------------------------------------------------------
What upstream shim tag is this starting from:
-------------------------------------------------------------------------------
HEAD of shim/15.2 branch (74b05de7d19fa4f462b6e228a8a03f8ee242b673)

-------------------------------------------------------------------------------
URL for a repo that contains the exact code which was built to get this binary:
-------------------------------------------------------------------------------
https://github.com/rhboot/shim/tree/74b05de7d19fa4f462b6e228a8a03f8ee242b673

-------------------------------------------------------------------------------
What patches are being applied and why:
-------------------------------------------------------------------------------
No additional patches are applied

-------------------------------------------------------------------------------
If bootloader, shim loading is, grub2: is CVE-2020-10713 fixed ?
-------------------------------------------------------------------------------
Yes, fixed by Ubuntu in 2.04-1ubuntu26.1, we are using 2.04-1ubuntu26.2

-------------------------------------------------------------------------------
If bootloader, shim loading is, grub2, and previous shims were trusting affected
by CVE-2020-10713 grub2:
* were old shims hashes provided to Microsoft for verification
  and to be added to future DBX update ?
* Does your new chain of trust disallow booting old, affected by CVE-2020-10713,
  grub2 builds ?
-------------------------------------------------------------------------------
First shim signing request so there are no previous versions available

-------------------------------------------------------------------------------
If your boot chain of trust includes linux kernel, is
"efi: Restrict efivar_ssdt_load when the kernel is locked down"
upstream commit 1957a85b0032a81e6482ca4aab883643b8dae06e applied ?
Is "ACPI: configfs: Disallow loading ACPI tables when locked down"
upstream commit 75b0cea7bf307f362057cc778efe89af4c615354 applied ?
-------------------------------------------------------------------------------
We are using upstream 5.9 kernel (currently rc5) so both commits are applied


-------------------------------------------------------------------------------
If you use vendor_db functionality of providing multiple certificates and/or
hashes please briefly describe your certificate setup. If there are whitelisted hashes
please provide exact binaries for which hashes are created via file sharing service,
available in public with anonymous access for verification
-------------------------------------------------------------------------------
Not using vendor_db

-------------------------------------------------------------------------------
What OS and toolchain must we use to reproduce this build?  Include where to find it, etc.  We're going to try to reproduce your build as close as possible to verify that it's really a build of the source tree you tell us it is, so these need to be fairly thorough. At the very least include the specific versions of gcc, binutils, and gnu-efi which were used, and where to find those binaries.
If possible, provide a Dockerfile that rebuilds the shim.
-------------------------------------------------------------------------------
The toolchain is based on Ubuntu 16.04 with gnu-efi 3.0.9-1 backported from Ubuntu 20.04

- gcc: 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.9unicon1)
- binutils: 2.26.1-1ubuntu1~16.04.3
- gnu-efi: 3.0.9-1

-------------------------------------------------------------------------------
Which files in this repo are the logs for your build?   This should include logs for creating the buildroots, applying patches, doing the build, creating the archives, etc.
-------------------------------------------------------------------------------
Build command: make EFI_PATH=/usr/lib VENDOR_CERT_FILE=UniconCodeSign-valid20230910.pem EFIDIR=eLux &> build.log
Log filename: build.log

-------------------------------------------------------------------------------
Add any additional information you think we may need to validate this shim
-------------------------------------------------------------------------------
None
