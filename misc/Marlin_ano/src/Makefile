ER = /dev/ttyACM0
BAUD = 115200
MCU = atmega2560
CFLAGS = -g -Os -Wall -fno-exceptions -ffunction-sections -fdata-sections -mmcu=$(MCU) \
				 	-DF_CPU=16000000L -DUSB_VID=null -DUSB_PID=null -DARDUINO=101 \
						-Iarduino/core -Iarduino/variants/eightanaloginputs
CPPFLAGS = $(CFLAGS)
ARDOBJ = wiring_shift.o wiring.o wiring_digital.o wiring_analog.o WInterrupts.o wiring_pulse.o \
				 	Print.o HardwareSerial.o new.o Stream.o main.o CDC.o WString.o USBCore.o IPAddress.o \
						HID.o WMath.o Tone.o

%.o: %.c
		avr-gcc $(CFLAGS) -c -o $@ $<

%.o: %.cpp
		avr-g++ $(CPPFLAGS) -c -o $@ $<

libcore.a: $(patsubst %,arduino/core/%,$(ARDOBJ))
		avr-ar cru $@ $(filter %.o,$^)

%.elf: %.o libcore.a
		avr-gcc -Os -Wl,--gc-sections -mmcu=$(MCU) -o $@ $^ -lm

%.eep: %.elf
		avr-objcopy -O ihex -j .eeprom --set-section-flags=.eeprom=alloc,load --no-change-warnings --change-section-lma .eeprom=0 $< $@

%.hex: %.elf
		avr-objcopy -O ihex -R .eeprom $< $@

%.upload: %.hex
		avrdude -p$(MCU) -carduino -P$(SER) -b$(BAUD) -D -Uflash:w:$<:i

%.hex: %.asm
		avra $< $@

clean:
		rm -f *.o *.elf *.hex *.eep
			rm -f arduino/core/*.o
				rm -f libcore.a
