HOST_OS := $(shell uname -s)

SRCS_adb += transport_usb.cpp
SRCS_adb += adb_listeners.cpp
SRCS_adb += adb_main.cpp
SRCS_adb += adb_utils.cpp
SRCS_adb += commandline.cpp
SRCS_adb += console.cpp
SRCS_adb += fdevent.cpp
SRCS_adb += file_sync_client.cpp
SRCS_adb += services.cpp
SRCS_adb += adb.cpp
SRCS_adb += adb_auth.cpp
SRCS_adb += transport_local.cpp
SRCS_adb += adb_auth_host.cpp
SRCS_adb += adb_client.cpp
SRCS_adb += adb_io.cpp
SRCS_adb += sockets.cpp
SRCS_adb += transport.cpp


ifeq ($(HOST_OS),Linux)
    SRCS_adb += get_my_path_linux.cpp
    USE_LIBUSB:=1
else ifeq ($(HOST_OS),Darwin)
    SRCS_adb += get_my_path_darwin.cpp
    SRCS_adb += usb_osx.cpp

    LIBS += -framework CoreFoundation -framework IOKit
else
    SRCS_adb += get_my_path_generic.cpp
    USE_LIBUSB:=1
endif

ifeq ($(USE_LIBUSB),1)
    SRCS_adb += usb_libusb.cpp

    CPPFLAGS += $(shell pkg-config --cflags libusb-1.0)
    LIBS += $(shell pkg-config --libs libusb-1.0)
endif

SRCS_libcutils += ../libcutils/load_file.c
SRCS_libcutils += ../libcutils/socket_inaddr_any_server.c
SRCS_libcutils += ../libcutils/socket_local_client.c
SRCS_libcutils += ../libcutils/socket_local_server.c
SRCS_libcutils += ../libcutils/socket_loopback_client.c
SRCS_libcutils += ../libcutils/socket_loopback_server.c
SRCS_libcutils += ../libcutils/socket_network_client.c

VPATH += ../base
SRCS_base += strings.cpp
SRCS_base += stringprintf.cpp

CPPFLAGS+= -DADB_HOST=1
CPPFLAGS += -I.
CPPFLAGS += -I../include
CPPFLAGS += -I../base/include
CXXFLAGS += -std=gnu++11

LIBS += -lcrypto -lpthread -lz

OBJS += $(SRCS_adb:.cpp=.o)
OBJS += $(SRCS_base:.cpp=.o)
OBJS += $(SRCS_libcutils:.c=.o)

all: adb

adb: $(OBJS)
	$(CXX) -o $@ $(CPPFLAGS) $(CFLAGS) $(CXXFLAGS) $(LDFLAGS) $(OBJS) $(LIBS)

clean:
	rm -f $(OBJS)
