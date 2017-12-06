BAMTOOLS_DIR := ./bamtools-2.3.0/
HTSLIB_DIR := ./htslib-1.3/

ABS_BAMTOOLS_DIR := $(realpath $(BAMTOOLS_DIR))
ABS_HTSLIB_DIR := $(realpath $(HTSLIB_DIR))

CXX := g++
CXXFLAGS :=-std=c++11 -Wno-deprecated -Wall -O3 -fexceptions -g -Wl,-rpath,$(ABS_BAMTOOLS_DIR)/lib/
INCLUDES := -I$(ABS_BAMTOOLS_DIR)/include/ -I$(ABS_HTSLIB_DIR)/ -L$(ABS_BAMTOOLS_DIR)/lib/ -L$(ABS_HTSLIB_DIR)/

all: bamtools htslib RLancet

.PHONY : RLancet
RLancet: Lancet.cpp align.cpp util.hh util.cpp sha256.hh sha256.cpp FET.hh ErrorCorrector.hh Mer.hh Ref.cpp Ref.hh ReadInfo.hh ReadStart.hh Transcript.hh Variant.hh Variant.cpp VariantDB.hh VariantDB.cpp Edge.cpp Edge.hh ContigLink.hh Node.cpp Node.hh Path.cpp Path.hh ContigLink.cpp Graph.cpp Graph.hh Microassembler.cpp Microassembler.hh
	$(CXX) $(CXXFLAGS) $(INCLUDES) Lancet.cpp Edge.cpp Node.cpp Graph.cpp Microassembler.cpp Ref.cpp Path.cpp ContigLink.cpp align.cpp util.cpp sha256.cpp VariantDB.cpp Variant.cpp -o RLancet.so $(ABS_HTSLIB_DIR)/libhts.a -lz -ldl -lbamtools -lpthread -fPIC -shared


.PHONY : bamtools
bamtools:
	mkdir $(ABS_BAMTOOLS_DIR)/build; cd $(ABS_BAMTOOLS_DIR)/build; cmake ..; make; cd ../

.PHONY : cleanbamtools
cleanbamtools:
	cd $(ABS_BAMTOOLS_DIR)/build; make clean; cd ../
	
.PHONY : htslib
htslib:
	cd $(ABS_HTSLIB_DIR); ./configure; make; cd ../

#.PHONY : clean
clean:
	 rm lancet src/lancet; rm -rf $(ABS_BAMTOOLS_DIR)/build; rm -rf $(ABS_BAMTOOLS_DIR)/include; rm -rf $(ABS_BAMTOOLS_DIR)/lib; rm -rf $(ABS_BAMTOOLS_DIR)/bin; cd $(ABS_HTSLIB_DIR); make clean;

