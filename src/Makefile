BASEDIR      = /usr/local/sce/ee
LIBDIR       = $(BASEDIR)/lib
INCDIR       = $(BASEDIR)/include -I/usr/local/sce/common/include

TARGET       = hello
OBJS         = crt0.o $(TARGET).o

LCFILE       = $(LIBDIR)/app.cmd
LIBS         = 

CROSS_PREFIX = ee
AS           = $(CROSS_PREFIX)-gcc
CC           = $(CROSS_PREFIX)-gcc
LD           = $(CROSS_PREFIX)-gcc
DVPASM       = $(CROSS_PREFIX)-dvp-as
OBJDUMP      = $(CROSS_PREFIX)-OBJDUMP
RM           = /bin/rm -f
RUN          = dsedb -nr run

CFLAGS       = -O2 -Wall -Werror -Wa,-al -fno-common -fno-strict-aliasing
ASFLAGS      = -c -xassembler-with-cpp -Wa,-al
LDFLAGS      = -Wl,-Map,$(TARGET).map -mno-crt0 -L$(LIBDIR) -lm

.SUFFIXES: .c

all: $(TARGET).elf

run: $(TARGET).elf
	$(RUN) $(TARGET).elf

$(TARGET).elf: $(OBJS) $(LIBS)
	$(LD) -o $@ -T $(LCFILE) $(OBJS) $(LIBS) $(LDFLAGS)

crt0.o: $(LIBDIR)/crt0.s
	$(AS) $(ASFLAGS) $(TMPFLAGS) -o $@ $< > $*.lst

.s.o:
	$(AS) $(ASFLAGS) $(TMPFLAGS) -I$(INCDIR) -o $@ $< > $*.lst

.c.o:
	$(CC) $(CFLAGS) $(TMPFLAGS) -I$(INCDIR) -c $< -o $*.o > $*.lst

clean:
	$(RM) *.o *.map *.lst *.elf