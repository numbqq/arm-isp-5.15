OUT_DIR ?= .
$(info "OUT_DIR : $(OUT_DIR)")

MEDIA_API_LOCAL_PATH := $(shell dirname $(lastword $(MAKEFILE_LIST)))
SRCS = $(shell find $(MEDIA_API_LOCAL_PATH) -name '*.cpp')
OBJS = $(patsubst %.cpp,%.o,$(SRCS))


ISP_ROOT_DIR := $(MEDIA_API_LOCAL_PATH)/..
LOCAL_INCLUDES := -I$(ISP_ROOT_DIR)/include/
LOCAL_INCLUDES+= -I$(ISP_ROOT_DIR)/sensor_calibration/imx290/
LOCAL_INCLUDES+= -I$(ISP_ROOT_DIR)/sensor_calibration/ov08a10/
LOCAL_INCLUDES+= -I$(ISP_ROOT_DIR)/sensor_calibration/imx415/
LOCAL_INCLUDES+= -I$(ISP_ROOT_DIR)/sensor_calibration/imx678/
LOCAL_INCLUDES+= -I$(ISP_ROOT_DIR)/sensor_calibration/imx585/
LOCAL_INCLUDES+= -I$(ISP_ROOT_DIR)/lens/dw9714/

CFLAGS += -I ./include/
CFLAGS += -I ./kernel-headers/
CFLAGS += $(LOCAL_INCLUDES)

LIBMEDIA_API = libmediaAPI.so


.PHONY: clean

# rules
all: $(LIBMEDIA_API)

%.o: %.cpp
	$(CC) -c -fPIC  $(CFLAGS) $^ -o $(OUT_DIR)/$@

$(LIBMEDIA_API): $(OBJS)
	$(CXX) -shared  -Wl,-soname,$(LIBMEDIA_API) -fPIC $(CFLAGS) $(patsubst %,$(OUT_DIR)/%,$^) -o $(OUT_DIR)/$(LIBMEDIA_API)

clean:
	rm -f $(patsubst %,$(OUT_DIR)/%,$(OBJS)) $(OUT_DIR)/$(LIBMEDIA_API)

$(shell mkdir -p $(OUT_DIR))
$(shell mkdir -p $(patsubst %,$(OUT_DIR)/%,$(dir $(SRCS))))