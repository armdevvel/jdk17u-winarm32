# JDK 17 for Windows RT armv7
## Prerequisites:
- Visual Studio Community 2022 (English ONLY! Uninstall non-English language packs)
- latest MSVC v143 2022 C++ build tools for ARM architecture, installed separately through Visual Studio Installer
- JDK 17 installed on your building machine
- Cygwin with additional packages: `autoconf`, `make`, `zip`, `unzip`
- VC Redistributable 2015/2017 ARMv7 installer for the target machine

#### To obtain the required VC Redistributable DLLs manually from an official source, follow these instructions:

On your target Windows RT machine:
1. Download and install the latest VC redistributable 2015 for ARMv7 from [here](https://download.microsoft.com/download/0/2/5/02596cd9-63cd-4c90-8e13-073ff0fe7fb5/vc_redist.arm.exe) (use Wayback Machine if the link is dead) or 2017 from unofficial source [here](https://files.open-rt.party/Software/Redistributables/VCRedist/vcredist_arm_vs2017.exe).
2. Open up C:\Windows\System32 and copy these dlls into a separate folder in the user space: `concrt140.dll`, `msvcp140.dll`, `vcamp140.dll`, `vccorlib140.dll`, `vcomp140.dll`, `vcruntime140.dll`.
3. Zip them and transfer them to your building machine.

## Building
#### <u>Use Cygwin Terminal to clone this project and execute commands below</u>
Running configure:

Replace `/cygdrive/c/path/to/msvc2015arm/` with a Cygwin path to your vcredist 2015/2017 DLL directory.
```
bash configure --host=arm-cygwin --with-toolchain-version=2022 "--with-tools-dir=/cygdrive/c/Program Files/Microsoft Visual Studio/2022/Community/VC/Auxiliary/Build" --with-msvcr-dll=/cygdrive/c/path/to/msvc2015arm/vcruntime140.dll --with-msvcp-dll=/cygdrive/c/path/to/msvc2015arm/msvcp140.dll
```

Building:
```
make jdk
```