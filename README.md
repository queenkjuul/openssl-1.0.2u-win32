# openssl-1.0.2u-win32
OpenSSL 1.0.2u with build modifications to work on Windows 98

Built using Visual C++ 6.0 on Windows XP. Binary tested on Windows 98SE. Should work on 95 with WINSOCK2? I'm not very familiar with 95.

Takes basic OpenSSL 1.0.2u, the last version to support 98, and makes two tiny changes:

- Disable IPv6
- Disable "Treat Warnings as Errors" compiler mode

## Binary Releases

See [the releases page](https://github.com/queenkjuul/openssl-1.0.2u-win32/releases) for a binary distribution.

## Building

It's surprisingly straightforward. If the below doesn't work, check out the [upstream docs](./INSTALL.W32), there's additional troubleshooting info there. This repo has already modified the flags for the `VC-WIN32` target - if you want to use a different target, you'll have to modify things yourself - see [this PR](https://github.com/queenkjuul/openssl-1.0.2u-win32/pull/1) for inspiration.

### Prerequisites

- Microsoft Visual C++ 6.0
- Perl 5.8+ (tested with [Strawberry Perl](https://strawberryperl.com/releases.html) 5.12)

### Procedure

1. Get a shell, ensure that perl is in your PATH (it should be if you used the Strawberry Perl MSI installer, and rebooted afterwards)
2. Load the Visual C++ environment - this is likely `"C:\Program Files\Microsoft Visual Studio\VC98\Bin\VCVARS32.BAT"`
3. Enter the openssl directory if you haven't already
4. `perl Configure VC-WIN32 no-asm --prefix=C:\openssl`
5. `ms\do_ms`
6. `nmake -f ms\ntdll.mak`
7. `nmake -f ms\ntdll.mak install` (optional, copies files to c:\openssl. manually add c:\openssl\bin to PATH if you want)
8. `nmake -f ms\ntdll.mak test` (for validation - all tests passed on XP SP3 with VC6 when I built it)
