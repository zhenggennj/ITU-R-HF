CC = gcc
# Use the following for testing
CFLAGS = -fPIC -Wall -Wextra -O0 -g  -fcommon
# Use the following for production
#CFLAGS = -fPIC -Wall -Wextra -O2

#LDFLAGS = -lm -ldl -z muldefs
LDFLAGS = -lm  
RM = rm -f
source_dir = ./

prefix ?= /usr/local
exec_prefix = $(prefix)
bindir = $(exec_prefix)/bin

TARGET = ITURNoise

SRCS = 	$(source_dir)ITURNoise.c

OBJS = $(SRCS:.c=.o)

.PHONY: all
all: ${TARGET}

$(TARGET): $(OBJS)
	$(CC) -o $@ $^ $(LDFLAGS)

$(SRCS:.c=.d):%.d:%.c
	$(CC) $(CFLAGS) -MM $< >$@
include $(SRCS:.c=.d)

.PHONY: clean
clean:
	-${RM} ${TARGET} ${OBJS} $(SRCS:.c=.d)

install: all
	install -d $(DESTDIR)$(bindir)/
	install -m 755 $(TARGET) $(DESTDIR)$(bindir)/ITURNoise
