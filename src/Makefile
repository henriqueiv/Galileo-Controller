TARGET=controller
UTILS=utils/conversion/types_conversion.c utils/conversion/measurement_conversion.c utils/datetime.c utils/utils.c
COMMONS=commons/errors.c
GALILEO=galileo/pwm.c galileo/adc_continuous.c galileo/eeprom.c
BUZZER=components/buzzer/buzzerconfig.c components/buzzer/buzzer.c
LED=components/led/ledconfig.c components/led/led.c
PUSHBUTTON=components/pushbutton/pushbuttonconfig.c components/pushbutton/pushbutton.c
POTENTIOMETER=components/potentiometer/potentiometer.c
SERVOMOTOR=components/servomotor/servomotor.c
DISPLAY=components/display/lcdconfig.c components/display/backlightconfig.c components/display/lcd.c
COMPONENTS=$(BUZZER) $(LED) $(PUSHBUTTON) $(POTENTIOMETER) $(SERVOMOTOR) $(DISPLAY)
SRCS=$(COMMONS) $(UTILS) $(GALILEO) $(COMPONENTS) $(TARGET).c

FLAGS=-MMD # -O2 cannot be used for using the Galileo's continuous mode
INCLUDE=-I. -I../include/
LIBDIR=-L../lib
LIBS=-lgalileo2

CC=$(CROSS_COMPILE)gcc
CFLAGS=$(FLAGS) $(INCLUDE)
LDFLAGS=$(LIBDIR) $(LIBS)

all: $(TARGET)

$(TARGET): $(SRCS:.c=.o)
	$(CC) -o $@ $^ $(LDFLAGS)

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

-include $(SRCS:.c=.d)

clean:
	rm -f *~ *.bak *.o *.d \
	components/display/*.d components/display/*.o \
	components/led/*.d components/led/*.o \
	commons/*.o commons/*.d \
	components/buzzer/*.d components/buzzer/*.o \
	components/pushbutton/*.d components/pushbutton/*.o \
	components/potentiometer/*.d components/potentiometer/*.o \
	components/servomotor/*.d components/servomotor/*.o \
	components/pushbutton/*.d components/pushbutton/*.o \
	utils/*.d utils/*.o utils/conversion/*.d utils/conversion/*.o \
	galileo/*.d galileo/*.o

distclean: clean
	rm -f $(TARGET)
