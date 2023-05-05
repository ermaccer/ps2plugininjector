# ps2plugininjector

An **experimental** attempt to add [PCSX2 Fork With Plugins](https://github.com/ASI-Factory/PCSX2-Fork-With-Plugins) plugin functionality on a real PlayStation 2.

Plugins allow to expand game code with new C functions that either replace originals or add ot them, this allows for 
more advanced mods and more!


# How it works?

A new section is added to the ELF executable containing plugin code, then the first EI call is replaced with a 
jump to the invoker function of the injected plugin.


# Disclaimer
Due to the fact that PS2 has a limited amount of ram (32MB), some games might be already using it all and
leave no place for any new code to be injected! Keep that in mind that "supported" games might be few.


# Usage

Run the executable without any params to get argument list

## Example command line
`ps2plugininjector -i MKDHookPS2.elf -o modded_mkd.elf SLUS_208.81`

# Samples

[MKDHookPS2](http://github.com/ermaccer/MKDHookPS2) - a plugin for MK Deception

[RandomLaddersMKA](https://github.com/ermaccer/RandomLaddersMKA) - a plugin for MK Armageddon

# Writing plugins

Plugins can only be written in pure C, C++ is not recommended and will definitely break your game.

## Guidelines

### Base Address
You need to find empty/unused space in memory and set that address as base address in the plugin make file, usually end of original executable + 0x10000 or 0x20000 should be just about enough - to be sure, check with PCSX2 memory view if your selected address is truly unused.


### Variables
Every variable needs to be initialized, do not leave uninitialized variables.

### Strings
All strings must be static to be used.

Do:
```cpp
static const char my_string[] = "Hello World";
my_string_function(my_string);
```
Don't:
```cpp
my_string_function("Hello World");
```

### Arrays, allocations
Static arrays have been tested and will work, any memory allocations have not been tested yet and theres a high chance they will break games, do it
at your own risk


### Summary
Basically you need to write plugins with code that only resides in .text section, that's the only section used for injecting - other sections are simply nullified/ignored on the PS2.


# Compatibility
A simple list of games that were tested and can (or not) have injected code - doesn't mean the amount of it is infinite.

| Name | Serial | Status |
|       ---       |       ---       |      ---       |
| Mortal Kombat Deception | SLUS-20881 |✅ Works  |
| Mortal Kombat Armageddon | SLUS-21410 |✅ Works  |
