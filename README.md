- Confirm the following are included in your repo, checking each box:

   - [x] completed README.md file with the necessary information
   - [x] shim.efi to be signed
   - [x] public portion of your certificate(s) embedded in shim (the file passed to VENDOR_CERT_FILE)
   - [ ] binaries, for which hashes are added to vendor_db ( if you use vendor_db and have hashes allow-listed )
   - [ ] any extra patches to shim via your own git tree or as files
   - [ ] any extra patches to grub via your own git tree or as files
   - [x] build logs
   - [x] a Dockerfile to reproduce the build of the provided shim EFI binaries

  *******************************************************************************

  ### What is the link to your tag in a repo cloned from rhboot/shim-review?

  *******************************************************************************

  https://github.com/howyar-dev/shim-review/tree/howyar-shim-x86_64-20260418

  *******************************************************************************

  ### What is the SHA256 hash of your final SHIM binary?

  *******************************************************************************

  150fdd153fbfa0b489afa85367cc0507ab778bad61529621b0dcf65ee10b726f

  *******************************************************************************

  ### What is the link to your previous shim review request (if any, otherwise N/A)?

  *******************************************************************************

  N/A

  *******************************************************************************

  ### If no security contacts have changed since verification, what is the link to your request, where they've been verified (if any, otherwise N/A)?

  *******************************************************************************

  N/A

  

  


  *******************************************************************************

  ### What organization or people are asking to have this signed?

  *******************************************************************************

  Organization name and website:  

  HOWYAR TECHNOLOGIES INC.

  https://www.howyar.com

  

  *******************************************************************************

  ### What's the legal data that proves the organization's genuineness?

  *******************************************************************************

  Company/tax register entries or equivalent:  
  (a link to the organization entry in your jurisdiction's register will do)  

  https://findbiz.nat.gov.tw 

  Since the website do not allowed sharing the link of the company directly, please search by entering the tax ID "80303961".

  

  The public details of both your organization and the issuer in the EV certificate used for signing .cab files at Microsoft Hardware Dev Center File Signing Services.  
  (**not** the CA certificate embedded in your shim binary)

  ```
  Issuer: C = US, O = "DigiCert, Inc.", CN = DigiCert Trusted G4 Code Signing RSA4096 SHA384 2021 CA1
  Subject: jurisdictionC = TW, businessCategory = Private Organization, serialNumber = 80303961, C = TW, ST = New Taipei City, O = Howyar Technologies Inc., CN = Howyar Technologies Inc.
  ```

  *******************************************************************************

  ### What product or service is this for?

  *******************************************************************************

  SysReturn Instant Recovery & Centralized Management System

  https://www.howyar.com/en-us/solution?id=sysreturn

  *******************************************************************************

  ### What's the justification that this really does need to be signed for the whole world to be able to boot it?

  *******************************************************************************

  Our recovery system requires redirecting the data that the operating system's boot files read and write under UEFI. Initially, we utilized the Microsoft signing process. However, as our projects expanded and client environments became increasingly complex, frequent compatibility adjustments to the UEFI became necessary.
  The turnaround time for Microsoft signing is too long for our frequent update cycles. During our last submission, the Microsoft auditor suggested we adopt the Shim solution. After a thorough internal evaluation, we have decided to transition to the Shim approach.

  *******************************************************************************

  ### Why are you unable to reuse shim from another distro that is already signed?

  *******************************************************************************

  To maintain compatibility with various operating systems, we avoid modifying the original OS boot flow. Our loader execution sequence is as follows: Motherboard Firmware → OurShim → osldr.efi → Original OS Bootloader (Shim, GRUB, bootmgfw, etc.).

  *******************************************************************************

  ### Who is the primary contact for security updates, etc.?

  *******************************************************************************


  - Name:  Rosie
  - Position:  CTO / Security Officer
  - Email address:  rosie@howyar.com
  - PGP key fingerprint:  1B036026FA5BC3D7B57DE51B661FD1707A1F87F4

  

  *******************************************************************************

  ### Who is the secondary contact for security updates, etc.?

  *******************************************************************************


  - Name: Fosi
  - Position: Technical Lead
  - Email address: fosi@howyar.com
  - PGP key fingerprint: BAFE05FF9A9387D03AF8429911AA6DAE967EFDC3

  

  *******************************************************************************

  ### Were these binaries created from the 16.1 shim release tar?

  *******************************************************************************

  Yes

  *******************************************************************************

  ### URL for a repo that contains the exact code which was built to result in your binary:

  *******************************************************************************

  https://github.com/howyar-dev/shim-source

  

  *******************************************************************************

  ### What patches are being applied and why:

  Mention all the external patches and build process modifications, which are used during your building process, that make your shim binary be the exact one that you posted as part of this application.

  *******************************************************************************

  No additional patches are applied. We use the original rhboot/shim version 16.1 source code, only embedding our own certificate via the VENDOR_CERT_FILE option.

  *******************************************************************************

  ### Do you have the NX bit set in your shim? If so, is your entire boot stack NX-compatible and what testing have you done to ensure such compatibility?

  See https://techcommunity.microsoft.com/t5/hardware-dev-center/nx-exception-for-shim-community/ba-p/3976522 for more details on the signing of shim without NX bit.

  *******************************************************************************

  Our Shim 16.1 is configured without the NX bit by default, consistent with current shim-review requirements. We have verified that our osldr.efi successfully loads original OS bootloaders across various UEFI environments (including Dell, Lenovo, and HP) without any NX-related compatibility issues. 
  Should NX support become a mandatory requirement for Shim in the future, we will adapt accordingly.

  

  *******************************************************************************

  ### Were old shims hashes provided to Microsoft for verification and to be added to future DBX updates?

  ### Does your new chain of trust disallow booting old GRUB2 builds affected by the CVEs?

  If you had no previous signed shim, say no here. Otherwise a simple _yes_ will do.

  *******************************************************************************


  We have never utilized any old versions of Shim. 
  Our new chain of trust operates as follows: Motherboard → OurShim → osldr.efi —(gBS->LoadImage)—> Original OS Bootloader. This process does not involve older versions of GRUB2, nor does it rely on any components affected by known CVEs.


  *******************************************************************************

  ### If your boot chain of trust includes a Linux kernel:

  ### Is upstream commit [1957a85b0032a81e6482ca4aab883643b8dae06e "efi: Restrict efivar_ssdt_load when the kernel is locked down"](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=1957a85b0032a81e6482ca4aab883643b8dae06e) applied?

  ### Is upstream commit [75b0cea7bf307f362057cc778efe89af4c615354 "ACPI: configfs: Disallow loading ACPI tables when locked down"](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=75b0cea7bf307f362057cc778efe89af4c615354) applied?

  ### Is upstream commit [eadb2f47a3ced5c64b23b90fd2a3463f63726066 "lockdown: also lock down previous kgdb use"](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=eadb2f47a3ced5c64b23b90fd2a3463f63726066) applied?

  Hint: upstream kernels should have all these applied, but if you ship your own heavily-modified older kernel version, that is being maintained separately from upstream, this may not be the case.  
  If you are shipping an older kernel, double-check your sources; maybe you do not have all the patches, but ship a configuration, that does not expose the issue(s).

  *******************************************************************************

  Not applicable. We do not directly load or boot any Linux kernels.

  *******************************************************************************

  ### How does your signed kernel enforce lockdown when your system runs with Secure Boot enabled?

  Hint: If it does not, we are not likely to sign your shim.

  *******************************************************************************

  We do not load any kernels. Instead, we use gBS->LoadImage to load the user's original OS bootloader (such as bootmgfw.efi, grub.efi, etc.). The responsibility for Secure Boot verification remains with the UEFI firmware and the original boot chain

  *******************************************************************************

  ### Do you build your signed kernel with additional local patches? What do they do?

  *******************************************************************************

  Not applicable. We do not build or boot any kernels.

  *******************************************************************************

  ### Do you use an ephemeral key for signing kernel modules?

  ### If not, please describe how you ensure that one kernel build does not load modules built for another kernel.

  *******************************************************************************

  No

  *******************************************************************************

  ### If you use vendor_db functionality of providing multiple certificates and/or hashes please briefly describe your certificate setup.

  ### If there are allow-listed hashes please provide exact binaries for which hashes are created via file sharing service, available in public with anonymous access for verification.

  *******************************************************************************

  Not applicable. We do not use the vendor_db option or any multi-certificate mechanisms.

  *******************************************************************************

  ### If you are re-using the CA certificate from your last shim binary, you will need to add the hashes of the previous GRUB2 binaries exposed to the CVEs mentioned earlier to vendor_dbx in shim. Please describe your strategy.

  This ensures that your new shim+GRUB2 can no longer chainload those older GRUB2 binaries with issues.

  If this is your first application or you're using a new CA certificate, please say so here.

  *******************************************************************************

  This is our initial Shim submission; we have no historical CA issues or prior vulnerabilities related to GRUB2.

  *******************************************************************************

  ### Is the Dockerfile in your repository the recipe for reproducing the building of your shim binary?

  A reviewer should always be able to run `docker build .` to get the exact binary you attached in your application.

  Hint: Prefer using *frozen* packages for your toolchain, since an update to GCC, binutils, gnu-efi may result in building a shim binary with a different checksum.

  If your shim binaries can't be reproduced using the provided Dockerfile, please explain why that's the case, what the differences would be and what build environment (OS and toolchain) is being used to reproduce this build? In this case please write a detailed guide, how to setup this build environment from scratch.

  *******************************************************************************

  Yes. The `shim-source` repository contains a Dockerfile that reproduces the exact build.

  - Base image: `ubuntu:22.04` (fixed)
  - Toolchain: `gcc`, `binutils`, `gnu-efi` from Ubuntu 22.04 (fixed versions)
  - Shim source: Official `shim-16.1.tar.bz2` tarball (SHA256 verified)

  To reproduce the build:

  ```bash
  git clone https://github.com/howyar-dev/shim-source.git
  cd shim-source
  docker build --output type=local,dest=./output .
  sha256sum output/shimx64.efi
  ```

  *******************************************************************************

  ### Which files in this repo are the logs for your build?

  This should include logs for creating the buildroots, applying patches, doing the build, creating the archives, etc.

  *******************************************************************************

  Build logs are located in the build-logs/ directory, including:"

    - `docker-build.log`

    

    

  *******************************************************************************

  ### What is the SHA256 hash of your final shim binary?

  *******************************************************************************

  150fdd153fbfa0b489afa85367cc0507ab778bad61529621b0dcf65ee10b726f

  

  *******************************************************************************

  ### How do you manage and protect the keys used in your shim?

  Describe the security strategy that is used for key protection. This can range from using hardware tokens like HSMs or Smartcards, air-gapped vaults, physical safes to other good practices.

  *******************************************************************************


  We utilize a dedicated, network-restricted machine to generate and embed certificates. 
  The private keys are stored in a Hardware Security Module (HSM) and require dual-authorization from two designated security officers for access. 
  Furthermore, all build processes are fully documented in audit logs.


  *******************************************************************************

  ### Do you use EV certificates as embedded certificates in the shim?

  A _yes_ or _no_ will do. There's no penalty for the latter.

  *******************************************************************************

  No

  

  *******************************************************************************

  ### Are you embedding a CA certificate in your shim?

  A _yes_ or _no_ will do. There's no penalty for the latter. However,
  if _yes_: does that certificate include the X509v3 Basic Constraints
  to say that it is a CA? See the [docs](./docs/) for more guidance
  about this.

  *******************************************************************************

  No

  *******************************************************************************

  ### Do you add a vendor-specific SBAT entry to the SBAT section in each binary that supports SBAT metadata ( GRUB2, fwupd, fwupdate, systemd-boot, systemd-stub, shim + all child shim binaries )?

  ### Please provide the exact SBAT entries for all binaries you are booting directly through shim.

  Hint: The history of SBAT and more information on how it works can be found [here](https://github.com/rhboot/shim/blob/main/SBAT.md). That document is large, so for just some examples check out [SBAT.example.md](https://github.com/rhboot/shim/blob/main/SBAT.example.md)

  If you are using a downstream implementation of GRUB2 (e.g. from Fedora or Debian), make sure you have their SBAT entries preserved and that you **append** your own (don't replace theirs) to simplify revocation.

  **Remember to post the entries of all the binaries. Apart from your bootloader, you may also be shipping e.g. a firmware updater, which will also have these.**

  Hint: run `objcopy --dump-section .sbat=/dev/stdout YOUR_EFI_BINARY` to get these entries. Paste them here. Preferably surround each listing with three backticks (\`\`\`), so they render well.

  

  No. We are using the default SBAT entries that come with Shim 16.1. We have not added any vendor-specific SBAT entries for our shim binary.

  Our bootloader (osldr.efi) is a minimal loader that only calls LoadImage/StartImage. It does not currently include SBAT metadata. We will add vendor-specific SBAT entries if required in the future.

  ```
  sbat,1,SBAT Version,sbat,1,https://github.com/rhboot/shim/blob/main/SBAT.md
  shim,4,UEFI shim,shim,1,https://github.com/rhboot/shim
  ```

  

  

  ### If you are using systemd-boot on arm64 or riscv, is the fix for [unverified Devicetree Blob loading](https://github.com/systemd/systemd/security/advisories/GHSA-6m6p-rjcq-334c) included?

  *******************************************************************************

  Not applicable. We only support the AMD64 (x86_64) architecture.

  *******************************************************************************

  ### What is the origin and full version number of your bootloader (GRUB2 or systemd-boot or other)?

  *******************************************************************************

  Our loader, osldr.efi, is a fully proprietary development. It is not based on GRUB2, systemd-boot, or any other existing bootloader frameworks.


  *******************************************************************************

  ### If your shim launches any other components apart from your bootloader, please provide further details on what is launched.

  Hint: The most common case here will be a firmware updater like fwupd.

  *******************************************************************************


  No. Shim only launches osldr.efi and does not initiate any other components.

  *******************************************************************************

  ### How do the launched components prevent execution of unauthenticated code?

  Summarize in one or two sentences, how your secure bootchain works on higher level.

  *******************************************************************************

  We do not load any kernels. Our loader, osldr.efi, utilizes the UEFI gBS->LoadImage and gBS->StartImage services to execute the original OS bootloader. 
  This process ensures that Secure Boot signature verification is strictly enforced by the UEFI firmware. We do not bypass or modify any existing verification logic.


  *******************************************************************************

  ### Does your shim load any loaders that support loading unsigned kernels (e.g. certain GRUB2 configurations)?

  *******************************************************************************

  No

  *******************************************************************************

  ### What kernel are you using? Which patches and configuration does it include to enforce Secure Boot?

  *******************************************************************************

  Not applicable. We do not load any kernels.

  *******************************************************************************

  ### What contributions have you made to help us review the applications of other applicants?

  The reviewing process is meant to be a peer-review effort and the best way to have your application reviewed faster is to help with reviewing others. We are in most cases volunteers working on this venue in our free time, rather than being employed and paid to review the applications during our business hours. 

  A reasonable timeframe of waiting for a review can reach 2-3 months. Helping us is the best way to shorten this period. The more help we get, the faster and the smoother things will go.

  For newcomers, the applications labeled as [*easy to review*](https://github.com/rhboot/shim-review/issues?q=is%3Aopen+is%3Aissue+label%3A%22easy+to+review%22) are recommended to start the contribution process.

  *******************************************************************************


  This is our first-time Shim submission, and we have not participated in other reviews yet. We are committed to assisting with future reviews for other applicants, particularly those within the system recovery software industry.	


  *******************************************************************************

  ### Add any additional information you think we may need to validate this shim signing application.

  *******************************************************************************

  Our product has supported UEFI since 2009, and we began using Microsoft signatures in 2015. Initially, our rapid iteration cycle and customized client requirements necessitated monthly updates. However, the 1-2 week turnaround for Microsoft signatures significantly hindered our deployment speed.
  At that time, before Shim became widely adopted, we implemented a workaround: a Microsoft-signed pre-loader that decrypted our main bootloader into memory and executed the PE program directly via EDK2 interfaces, bypassing LoadImage. In 2024, recognizing the security vulnerabilities inherent in this approach, we reverted to directly signing our bootloader. Consequently, we faced the same bottlenecks once again—long signing delays caused client dissatisfaction when urgent bug fixes were required.
  During a recent review, the Microsoft UEFI Team suggested we adopt the Shim mechanism. Upon deeper investigation, we realized that Shim is the ideal solution for our needs, balancing both security and update efficiency. Therefore, we are submitting this application.
