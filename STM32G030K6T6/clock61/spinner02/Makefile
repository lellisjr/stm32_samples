
ARMGNU = arm-none-eabi
#ARMGNU = arm-linux-gnueabi

AOPS = --warn --fatal-warnings -mcpu=cortex-m0
COPS = -Wall -O2 -nostdlib -nostartfiles -ffreestanding 
 -mcpu=cortex-m0

all : spinner02.bin

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list
	rm -f buildheader

#---------------------------------


twostuff.h : buildheader.c
	gcc buildheader.c -o buildheader
	./buildheader > twostuff.h

flash.o : flash.s
	$(ARMGNU)-as $(AOPS) flash.s -o flash.o

spinner02.o : spinner02.c twostuff.h
	$(ARMGNU)-gcc $(COPS) -mthumb -mcpu=cortex-m0 -march=armv6-m -c spinner02.c -o spinner02.o

spinner02.bin : flash.ld flash.o spinner02.o
	$(ARMGNU)-ld -o spinner02.elf -T flash.ld flash.o spinner02.o
	$(ARMGNU)-objdump -D spinner02.elf > spinner02.list
	$(ARMGNU)-objcopy spinner02.elf spinner02.bin -O binary

