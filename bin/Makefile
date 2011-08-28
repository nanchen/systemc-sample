TARGET_ARCH = linux
SYSTEMC = /home/nan/dev/systemc-2.2.0

CC     = g++
OPT    = -O0
DEBUG  = -g
OTHER  = # -Wall -Wno-deprecated
CFLAGS = $(OPT) $(OTHER) # $(DEBUG)

VPATH = ../src:.

SRCS := $(wildcard ../src/*.cpp)
OBJS = $(subst ../src/,,$(SRCS:.cpp=.o))

INCDIR = -I. -I.. -I../src -I$(SYSTEMC)/include 
LIBDIR = -L. -L.. -L../src -L$(SYSTEMC)/lib-$(TARGET_ARCH) 

LIBS = -lsystemc

.SUFFIXES: .cpp .o 

#noxim: $(OBJS) $(SYSTEMC)/lib-$(TARGET_ARCH)/libsystemc.a /home/nan/chen-work/c-data-structures-analysis/bin/Debug/libc-data-structures-analysis.a
#	$(CC) $(CFLAGS) $(INCDIR) $(LIBDIR) -fexceptions -o $@ $(OBJS) $(LIBS) 2>&1 | c++filt

all: hello first_counter ports_access

hello: hello.o
	$(CC) $(CFLAGS) $(INCDIR) $(LIBDIR) -o $@ hello.o $(LIBS)

first_counter: first_counter.o first_counter_tb.o
	$(CC) $(CFLAGS) $(INCDIR) $(LIBDIR) -o $@ first_counter.o first_counter_tb.o $(LIBS)

ports_access: ports_access.o
	$(CC) $(CFLAGS) $(INCDIR) $(LIBDIR) -o $@ ports_access.o $(LIBS)


.cpp.o:
	$(CC) $(CFLAGS) $(INCDIR) -c -g $<

%.d: %.cpp
	@set -e; rm -f $@; \
         $(CC) -M $(CFLAGS) $< >; $@.$$$$; \
         sed 's,\($*\)\.o[ :]*,\1.o $@ : ,g' < $@.$$$$ >; $@; \
         rm -f $@.$$$$

clean:
	rm -f $(OBJS)

#include ./Makefile.deps

