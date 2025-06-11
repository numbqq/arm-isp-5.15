OUT_DIR ?= .
$(info "OUT_DIR : $(OUT_DIR)")

TUNING_SUBDIR := $(shell dirname $(lastword $(MAKEFILE_LIST)))
SRCS = $(shell find $(TUNING_SUBDIR) -name '*.cpp')
OBJS = $(patsubst %.cpp,%.o,$(SRCS))

#LOCAL_PATH := $(shell dirname $(lastword $(MAKEFILE_LIST)))

ISP_ROOT_DIR := $(TUNING_SUBDIR)/..
LOCAL_INCLUDES := -I$(ISP_ROOT_DIR)/include/

CFLAGS += -I ./include/
CFLAGS += -I ./kernel-headers/
CFLAGS += $(LOCAL_INCLUDES)

LIBTUNING = libtuning.so


.PHONY: clean

# rules
all: $(LIBTUNING)
	@echo "CXX is: $(CXX)"

%.o: %.cpp
#%.o: $(TUNING_SUBDIR) %.cpp
	$(CC) -c -fPIC  $(CFLAGS) $^ -o $(OUT_DIR)/$@

$(LIBTUNING): $(OBJS)
	$(CXX) -shared  -Wl,-soname,$(LIBTUNING) -fPIC $(CFLAGS) $(patsubst %,$(OUT_DIR)/%,$^) -o $(OUT_DIR)/$(LIBTUNING)

clean:
	rm -f $(patsubst %,$(OUT_DIR)/%,$(OBJS)) $(OUT_DIR)/$(LIBTUNING)

$(shell mkdir -p $(OUT_DIR))
$(shell mkdir -p $(patsubst %,$(OUT_DIR)/%,$(dir $(SRCS))))