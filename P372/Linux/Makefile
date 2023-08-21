CC = gcc
source_dir = ../Src/P372/
bin_dir = ../Bin/
# Use the following for testing
CFLAGS = -fPIC -Wall -Wextra -O0 -g -I$(source_dir) -fcommon
# Use the following for production
#CFLAGS = -fPIC -Wall -Wextra -O2 -I$(source_dir)

#LDFLAGS = -shared -lm -ldl -z muldefs
LDFLAGS = -shared -lm  
RM = rm -f
#TARGET_LIB = libp372.so
TARGET_LIB = p372.dll

prefix ?= /usr/local
exec_prefix = $(prefix)
#libdir = $(exec_prefix)/lib
bindir = $(exec_prefix)/bin

SRCS = $(source_dir)InitializeNoise.c \
       $(source_dir)Noise.c \
       $(source_dir)NoiseMemory.c \
       $(source_dir)MakeNoise.c

OBJS = $(SRCS:.c=.o)

.PHONY: all
all: ${TARGET_LIB}

$(TARGET_LIB): $(OBJS)
	$(CC) -o $@ $^ $(LDFLAGS)

$(SRCS:.c=.d):%.d:%.c
	$(CC) $(CFLAGS) -MM $< >$@
include $(SRCS:.c=.d)

.PHONY: clean

clean:
	${RM} ${OBJS} $(SRCS:.c=.d)
	${RM} ${TARGET_LIB}

install: all
	install -d $(DESTDIR)$(bindir)/
	install -m 755 $(TARGET_LIB) $(DESTDIR)$(bindir)/$(TARGET_LIB)
