### HOW TO MAKE CHANGES ###
After making changes to the boot.s file:
- run `i686-elf-as boot.s -o boot.o`

After making changes to the kernel.cpp file:
- run `i686-elf-g++ -c kernel.cpp -o kernel.o -ffreestanding -O2 -Wall -Wextra -fno-exceptions -fno-rtti`

After changes to either files and/or changing the linker.ld file:
- run `i686-elf-g++ -T linker.ld -o myos.bin -ffreestanding -O2 -nostdlib boot.o kernel.o -lgcc`

To verify multiboot:
- run `grub2-file --is-x86-multiboot myos.bin`
- then run `echo $?` 0 = sucess; 1 = failed

To build the iso file:
- run this series of commands ```mkdir -p isodir/boot/grub
cp myos.bin isodir/boot/myos.bin
cp grub.cfg isodir/boot/grub/grub.cfg
grub-mkrescue -o myos.iso isodir ```


### BOOT WITH qemu-system-i386 -cdrom myos.iso ###
