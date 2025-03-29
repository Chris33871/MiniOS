# VERY SMALL OPERATING SYSTEM

## MAKING CHANGES ##
After making changes to the boot.s file:
- run `i686-elf-as boot.s -o boot.o`

After making changes to the kernel.cpp file:
- Compile using: `i686-elf-gcc -c kernel.c -o kernel.o -std=gnu99 -ffreestanding -O2 -Wall -Wextra`

After changes to either files and/or changing the linker.ld file:
- Compile using `i686-elf-gcc -T linker.ld -o myos.bin -ffreestanding -O2 -nostdlib boot.o kernel.o -lgcc`

To check whether a file has a valid multiboot version 1 header:
- run `grub2-file --is-x86-multiboot myos.bin`
- then run `echo $?` to get the status. 0 = sucess; 1 = failed

To build the iso file:
- run this series of commands
```
mkdir -p isodir/boot/grub
cp myos.bin isodir/boot/myos.bin
cp grub.cfg isodir/boot/grub/grub.cfg
grub2-mkrescue -o myos.iso isodir 
```

Boot using QEMU with the command:
- `qemu-system-i386 -cdrom myos.iso`


### Useful information:
boot.s - kernel entry point that sets up the processor environment
kernel.c - your actual kernel routines
linker.ld - for linking the above files
