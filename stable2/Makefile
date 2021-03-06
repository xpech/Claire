# ************************************************************
# *  Makefile for the CLAIRE system.                         *
# *  UNIX version  - CLAIRE 3.3                              *
# ************************************************************

all: Darwin-i386-g++4.2.1/cclaire

# -------------------------------------------
# |      1. directories                      |
# -------------------------------------------

# directories
Dl = Darwin-i386-g++4.2.1
Ds = csrc
Dh = include

#utilities
CXX = g++

# this line is system-dependent ! you may need to edit it ...
CXXFLAGS = -DCLDEBUG -g -Wno-write-strings -I$(Dh)



$(Dl)/Kernel.o:	$(Ds)/Kernel.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Kernel.o -c $(Ds)/Kernel.cpp

$(Dl)/Console.o:	$(Ds)/clConsole.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Console.o -c $(Ds)/clConsole.cpp

$(Dl)/noConsole.o:	$(Ds)/clNoConsole.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/noConsole.o -c $(Ds)/clNoConsole.cpp

$(Dl)/wclConsole.o:	$(Ds)/wclConsole.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/wclConsole.o -c $(Ds)/wclConsole.cpp

$(Dl)/Core.o:	$(Ds)/Core.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Core.o -c $(Ds)/Core.cpp

$(Dl)/Language.o:	$(Ds)/Language.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Language.o -c $(Ds)/Language.cpp

$(Dl)/Reader.o:	$(Ds)/Reader.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Reader.o -c $(Ds)/Reader.cpp

$(Dl)/Optimize.o:	$(Ds)/Optimize.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Optimize.o -c $(Ds)/Optimize.cpp

$(Dl)/Generate.o:	$(Ds)/Generate.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Generate.o -c $(Ds)/Generate.cpp

$(Dl)/Serialize.o:	$(Ds)/Serialize.cpp
	$(CXX) $(CXXFLAGS) -o $(Dl)/Serialize.o -c $(Ds)/Serialize.cpp

sclaire-s.o:	$(Ds)/sclaire-s.cpp
	$(CXX) $(CXXFLAGS) -o sclaire-s.o -c $(Ds)/sclaire-s.cpp

# +----------------------------------------------------------------+
# |  How to create the wcl cgi                                     |
# +----------------------------------------------------------------+

mod_wcl: cgi/mod_wcl.c
	apxs -a -i -c cgi/mod_wcl.c

# +----------------------------------------------------------------+
# |  How to create a claire compiler                               |
# +----------------------------------------------------------------+

LIBS_claire = $(Dl)/Kernel.o \
  $(Dl)/Console.o \
  $(Dl)/Core.o \
  $(Dl)/Language.o \
  $(Dl)/Reader.o \
  $(Dl)/Optimize.o \
  $(Dl)/Generate.o \
  $(Dl)/Serialize.o

Darwin-i386-g++4.2.1/dummy:
	mkdir -p Darwin-i386-g++4.2.1
	touch Darwin-i386-g++4.2.1/dummy

$(Dl)/sclaire: Darwin-i386-g++4.2.1/dummy $(LIBS_claire) $(Dl)/noConsole.o $(Dl)/wclConsole.o sclaire-s.o
	$(CXX)  -g  -o $(Dl)/sclaire -lpthread -ldl  -ledit  sclaire-s.o $(LIBS_claire)


# +----------------------------------------------------------------+
# |  How to create a proper version of claire                      |
# +----------------------------------------------------------------+

$(Dl)/cclaire: ccmain.cl $(Dl)/sclaire
	./$(Dl)/sclaire -O -m Compile -m Serialize -cx ccmain -o cclaire
	cp $(Dl)/cclaire claire
	

# +----------------------------------------------------------------+
# |  How to install claire in /usr/local                           |
# +----------------------------------------------------------------+

install: $(Dl)/cclaire
	./$(Dl)/sclaire -f init -v 0 -f install -q

