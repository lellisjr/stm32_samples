
ARMGNU = arm-none-eabi
#ARMGNU = arm-linux-gnueabi

AOPS = --warn --fatal-warnings -mcpu=cortex-m3
COPS = -Wall -O2 -nostdlib -nostartfiles -ffreestanding 
 -mcpu=cortex-m0

all : notmain.bin

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list
	rm -f *.bc
	rm -f *.opt.s
	rm -f *.norm.s
	rm -f *.hex

#---------------------------------

flash.o : flash.s
	$(ARMGNU)-as $(AOPS) flash.s -o flash.o

notmain.o : notmain.c
	$(ARMGNU)-gcc $(COPS) -mthumb -mcpu=cortex-m0 -march=armv6-m -c notmain.c -o notmain.o

notmain.bin : flash.ld flash.o notmain.o
	$(ARMGNU)-ld -o notmain.elf -T flash.ld flash.o notmain.o
	$(ARMGNU)-objdump -D notmain.elf > notmain.list
	$(ARMGNU)-objcopy notmain.elf notmain.bin -O binary

