#---------------------------------------------------------------------------------
# Clear the implicit built in rules
#---------------------------------------------------------------------------------
.SUFFIXES:
#---------------------------------------------------------------------------------
ifeq ($(strip $(PS3DEV)),)
$(error "Please set PS3DEV in your environment. export PS3DEV=<path>")
endif

CC	:=	gcc

CFLAGS	:=	-Wall -Wno-char-subscripts -O2 -s

ifeq ($(strip $(PS3DEV)),)
  ifeq ($(strip $(DEVKITPS3)),)
    export PS3DEV := /usr/local/ps3dev
  else
    export PS3DEV := $(DEVKITPS3)
  endif
endif

ifneq (,$(findstring MINGW,$(shell uname -s)))
	exeext		:= .exe
endif

ifneq (,$(findstring CYGWIN,$(UNAME)))
	exeext		:= .exe
endif

ifneq (,$(findstring Darwin,$(shell uname -s)))
	SDK	:=	/Developer/SDKs/MacOSX10.4u.sdk
	CFLAGS += -mmacosx-version-min=10.4 -isysroot $(SDK) -Wl,-syslibroot,$(SDK) -arch i386 -arch ppc
endif

TARGETS	:=	$(patsubst %.c,%$(exeext),$(wildcard *.c)) \
		$(patsubst %.cpp,%$(exeext),$(wildcard *.cpp))


all:	$(TARGETS)

clean:
	@echo clean ...
	@rm -f $(TARGETS)

%$(exeext)	:: %.c
	@$(CC) $< -o $@ $(CFLAGS)

%$(exeext)	:: %.cpp
	@$(CXX) $< -o $@ $(CFLAGS)

install: all
	@echo Installing $(TARGETS)
	@[ -d $(PS3DEV)/host/bin ] || mkdir -p $(PS3DEV)/host/bin
	@install -m 755 $(TARGETS) $(PS3DEV)/host/bin
