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
todo