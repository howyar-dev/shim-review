# Shim Review for Howyar Technologies Inc. - SysReturn

## Overview
SysReturn Instant Recovery & Centralized Management System
https://www.howyar.com/en-us/solution?id=sysreturn

## Version Information
- Shim Version: 16.1
- Architecture: x86_64
- Certificate: See vendor.cer
- Default Loader: `\osldr.efi`

## Build Instructions
```bash
docker build --output type=local,dest=./output .
```

## Verification
```bash
sha256sum shimx64.efi
```
```text
150fdd153fbfa0b489afa85367cc0507ab778bad61529621b0dcf65ee10b726f  shimx64.efi
```

## SBAT Output
```bash
objcopy --dump-section .sbat=/dev/stdout shimx64.efi 2>/dev/null
```
```text
sbat,1,SBAT Version,sbat,1,https://github.com/rhboot/shim/blob/main/SBAT.md
shim,4,UEFI shim,shim,1,https://github.com/rhboot/shim
```

## Security Contacts
- Primary: rosie@howyar.com (PGP: 1B036026FA5BC3D7B57DE51B661FD1707A1F87F4)
- Secondary: fosi@howyar.com (PGP: BAFE05FF9A9387D03AF8429911AA6DAE967EFDC3)

## Files Included
- `shimx64.efi` - Built shim binary
- `vendor.cer` - Embedded certificate
- `Dockerfile` - Reproducible build environment
- `build-logs/` - Complete build logs

## Build Configuration
- Source: Unaltered Shim 16.1 from official tarball
- Certificate: Embedded `vendor.cer`
- Default Loader: Set to `\\osldr.efi` via `DEFAULT_LOADER` variable
- SBAT: Enabled (`ENABLE_SBAT=1`)
