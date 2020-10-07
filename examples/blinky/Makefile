CC = ../../xtensa-lx106-elf/bin/xtensa-lx106-elf-gcc
CFLAGS = -Os -I. -mlongcalls -ffunction-sections -fdata-sections
LDLIBS = -Wl,-gc-sections -ffunction-sections -fdata-sections -nostdlib -Wl,--start-group -lmain -lnet80211 -lwpa -llwip -lpp -lphy -lc -Wl,--end-group -lgcc
LDFLAGS = -Teagle.app.v6.ld

blinky-0x00000.bin: blinky
	esptool.py elf2image $^

blinky: blinky.o

blinky.o: blinky.c

flash: blinky-0x00000.bin
	esptool.py --port  /dev/ttyUSB0 --baud 115200 write_flash 0 blinky-0x00000.bin 0x10000 blinky-0x10000.bin

clean:
	rm -f blinky blinky.o blinky-0x00000.bin blinky-0x10000.bin
