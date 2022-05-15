---
id: 2650
title: 'Compiling with QtSDK, Madde and MinGW Makefiles'
date: '2011-07-15T17:31:56+03:00'
author: Summeli
layout: post
guid: 'http://www.summeli.fi/?p=2650'
permalink: /2650/
aktt_notify_twitter:
    - 'yes'
aktt_tweeted:
    - '1'
categories:
    - 'Meego Development'
tags:
    - compiling
    - gcc
    - madde
    - MinGW
    - 'Qt Development'
    - QtSDK
---

I received N950 from Nokia this monday, and I started porting the antsnes to Meego right away.  
I decided to compile my emulators for Meego in the same way as I did for Symbian. I’m creating a static lib from the emulator core, and then I’m linking into that static lib from my UI code. The idea in here is that, I can make all kinds of special tricks when compiling the emulator core, and then use the standard Qt’s pro-file to compile the UI part. To accomplis this, I made a similar MinGW makefile for Madde, as I used with Symbian.  

### INSTALLATION   
Here are the instructions to use this environment.

1. Install [MSYS](http://www.mingw.org/wiki/msys)
2. Set environment variable MADDE\_PATH to point into your Madde installation. It should point into it in msys format, for example /e/QtSDK/Madde

### BUILDING WITH THE MAKEFILE     
You’ll need two files: Makefile and config.mk in***myapp/gms*** path. You should also make folders ***myapp/gms/dist/gcce*** and***myapp/gms/obj/gcce*** .  
After all these done, you could change your working directory into the build home by “***cd /c/myapp/gms***“. Then use the following commands to build. - “***make debug***” will do the debug build,
- **“make release”** will do the release build
- **“make clean”** will do the clean

A sample of config.mk is shown on below. The syntax is pretty easy to undertand, no big suprises in here

```
PROJECT_NAME = myproject
USERINCLUDE = ../inc
CXXSRCS = \
 myapp.cpp \
 $(NULL)
CSRCS = \
 main.c \
 $(NULL)
ASRCS = \
 my_asm_optimized_source.S \
 $(NULL)
```

And here’s a sample of a Makefile

```
MADDE_GCC_INSTALL_PATH =$(MADDE_PATH)/toolchains/arm-2009q3-67-arm-none-linux-gnueabi-i586-mingw32msvc/arm-2009q3-67/bin
MADDE_INCLUDE = $(MADDE_PATH)/sysroots/harmattan-nokia-meego-arm-sysroot-1122-slim/usr/include
PATH := $(MADDE_GCC_INSTALL_PATH):$(PATH)
SYSINCLUDE = $(MADDE_PATH)/sysroots/harmattan-nokia-meego-arm-sysroot-1122-slim/usr/lib/gcc/arm-linux-gnueabi/4.4/include \
$(MADDE_INCLUDE)
#Macros for compilation process
GCC_MACRO = -D__GCCE__ -D__MARM__ -D__MARM_ARMV5__ -D__EABI__
CPP_MACRO = -D__SUPPORT_CPP_EXCEPTIONS__
EXE_MACRO = -D__EXE__
REL_MACRO = -DNDEBUG
DEB_MACRO = -D_DEBUG
UNICODE_MACRO = -D_UNICODE
GCC_WARNING_FLAGS = -Wall -Wno-unknown-pragmas
CPP_ARGS = -undef -M -nostdinc
# paths
SRC_PATH = ../
OBJ_BASE = obj
DIST_BASE = dist
include config.mk
check:
	@echo 'MADDE_PATH is' $(MADDE_PATH)
	@echo 'MADDE_INCLUDE is ' $(MADDE_INCLUDE)
	@echo 'MADDE_GCC_INSTALL_PATH is ' $(MADDE_GCC_INSTALL_PATH)
	@echo 'PATH is ' $(PATH)
	@echo '==============================================================='
preGCC:
  CC = arm-none-linux-gnueabi-gcc
  CXX = arm-none-linux-gnueabi-g++
  LD = arm-none-linux-gnueabi-ld
  AS = arm-none-linux-gnueabi-as
  AR = arm-none-linux-gnueabi-ar
  DIST_PATH = $(DIST_BASE)/gcce
  OBJ_PATH = $(OBJ_BASE)/gcce
  TARGET_MACRO = $(GCC_MACRO) $(GCC_WARNING_FLAGS)
preDEBUG:
   COMPFLAGS = -march=armv7-a -O0 -mapcs -pipe -nostdinc -c -g \
   -MD $(DEB_MACRO)
preREL:
   COMPFLAGS = -march=armv7-a -O2 -mapcs -pipe -nostdinc -c \
   -MD $(REL_MACRO) -include $(EPOCROOT2)/include/gcce/gcce.h
preALL:
  CFLAGS += $(COMPFLAGS) $(UNICODE_MACRO) $(TARGET_MACRO) \
	$(EXE_MACRO) $(addprefix -D ,$(PRJ_MACRO)) \
  -I $(SRC_PATH) $(addprefix -I ,$(USERINCLUDE)) $(addprefix -I ,$(SYSINCLUDE))
  CXXFLAGS = $(CFLAGS) -Wno-ctor-dtor-privacy -x c++ $(CPP_MACRO)
  C_OBJS = $(patsubst %.c,$(OBJ_PATH)/%.o,$(CSRCS))
  CXX_OBJS = $(patsubst %.cpp,$(OBJ_PATH)/%.o,$(CXXSRCS))
  A_OBJS =  $(patsubst %.S,$(OBJ_PATH)/%.o,$(ASRCS))
  BIN_TARGET = $(DIST_PATH)/$(PROJECT_NAME).a
  ASFLAGS = -mfloat-abi=soft
  COPYLIB = cp $(DIST_PATH)/$(PROJECT_NAME).a ../$(PROJECT_NAME).a
$(CXX_OBJS): $(OBJ_PATH)/%.o : $(SRC_PATH)/%.cpp
	$(CXX) $(CXXFLAGS) -o $@ $<
$(C_OBJS): $(OBJ_PATH)/%.o : $(SRC_PATH)/%.c
	$(CC) $(CFLAGS) -o $@ $<
$(A_OBJS): $(OBJ_PATH)/%.o : $(SRC_PATH)/%.S
	$(CC) -c -o $@ $^
$(BIN_TARGET): $(C_OBJS) $(CXX_OBJS) $(A_OBJS)
	$(AR) rsc $(BIN_TARGET) $(C_OBJS) $(CXX_OBJS) $(A_OBJS)
	$(COPYLIB)
cleang: check preGCC preALL
	rm -rf $(C_OBJS) $(CXX_OBJS) $(A_OBJS)
	rm -rf $(BIN_TARGET)
cleanw: check
buildw: check
clean: cleang
debug: check preGCC preDEBUG preALL $(BIN_TARGET)
release: check preGCC preREL preALL $(BIN_TARGET)
```

### DEBUGGING     
The QtCreator seems to be able to find the code without any help, so no special tricks required in here.
