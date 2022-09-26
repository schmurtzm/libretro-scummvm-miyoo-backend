# libretro-scummvm-backend   - edited for Miyoo Mini
Libretro backend for ScummVM which can be added to backends/platform folder of ScummVM base to build a Libretro core of ScummVM. The intention is be able to apply the backend without adjusting any of base ScummVM.

This repo is based on [StupidHoroscope/libretro-scummvm-miyoo-backend](https://github.com/StupidHoroscope/libretro-scummvm-miyoo-backend) which is a fork of the [diablodiab/libretro-scummvm-backend](https://github.com/diablodiab/libretro-scummvm-backend) repo.

For easy use it has been added in [schmurtzm/ScummVM-MiyooMini](https://github.com/schmurtzm/ScummVM-MiyooMini) repo as submodule.
It allows to generate an up to date Retroarch core from current version of ScummVM (v2.6 stable or v2.7 dev).

This ScummVM core is more up to date than the current official libretro core so it supports more games including 2.5D games like Grim Fandango (About 385 in v2.7 vs 298 games for the v2.1.1).


Comparing the official diablodiab's backend, this repo contains some optimizations for low power devices like the Miyoo Mini handheld : 
- a better mouse cursor acceleration to be use with the D-Pad of the Miyoo Miyoo
- a new core option allows to choose a target FPS which impacts audio buffer and allow to have less audio stuttering.
- a makefile modified for Miyoo Mini


## How to use

```
git clone https://github.com/schmurtzm/ScummVM-MiyooMini.git
cd ScummVM-MiyooMini
git submodule init 
git submodule update
cd backends/platform/libretro/build
make platform=miyoomini -j$(nproc)
```
As there are very few differences with the official ScummVM repo you could also do this : 

1. Clone official ScummVM base ([schmurtzm/ScummVM-MiyooMini](https://github.com/schmurtzm/ScummVM-MiyooMini))
2. Go to subfolder scummvm/backends/platform
3. Clone [schmurtzm/libretro-scummvm-miyoo-backend](https://github.com/schmurtzm/libretro-scummvm-miyoo-backend) to folder "libretro"
4. Go to folder scummvm/backends/platform/libretro/build
5. Compile libretro-scummvm core

## Updating
When updating ScummVM, it's important to rebuild [scummvm.zip](aux-data/scummvm.zip) so that any auxiliary data is bundled in. The compile the new scummvm.zip, run the following command:

```
cd backends/platform/libretro/aux-data
./bundle_aux_data.bash
```
These extra files can be unziped in BIOS folder of the Miyoo Mini. 
This archive contains themes and files required to make some engines work (like kyra.dat for westwood games).

---




## Patches
Some issues cannot be fixed without making adjustments to base ScummVM. These are maintained as patches in the patches folder and can be applied before compiling if needed.

#### android_fix_hopkins.patch
Fixes a timing issue with fading on Android causing Hopkins FBI to crash at the title screen

#### android_macos_fix_ags.patch
Fixes issues with the AGS engine on Android and macOS when using -O2 and -O3 compiler performance optimization

#### macos_fix_androidbuilding.patch
Fixes issues with compilation for Android on macOS where input limit for commands is exceeded

#### macos_fix_ultima.patch
Fixes struct packing issues when compiling Ultima engine on macOS Monterey



