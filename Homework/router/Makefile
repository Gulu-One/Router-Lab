CXX ?= g++
LAB_ROOT ?= ../..
BACKEND ?= LINUX
CXXFLAGS ?= --std=c++11 -I $(LAB_ROOT)/HAL/include -DROUTER_BACKEND_$(BACKEND) -Wno-psabi
LDFLAGS ?= -lpcap

.PHONY: all clean
all: router

clean:
	rm -f *.o router std

%.o: %.cpp
	$(CXX) $(CXXFLAGS) -c $^ -o $@

hal.o: $(LAB_ROOT)/HAL/src/linux/router_hal.cpp $(LAB_ROOT)/HAL/src/linux/platform/standard.h
	$(CXX) $(CXXFLAGS) -c $< -o $@

router: main.o hal.o protocol.o checksum.o lookup.o forwarding.o
	$(CXX) $^ -o $@ $(LDFLAGS) 
