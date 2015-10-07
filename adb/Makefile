CXXSRCS += adb.cpp
CXXSRCS += adb_main.cpp
CXXSRCS += adb_utils.cpp
CXXSRCS += adb_auth.cpp
CXXSRCS += adb_auth_host.cpp
CXXSRCS += adb_client.cpp
CXXSRCS += adb_io.cpp
CXXSRCS += adb_listeners.cpp
CXXSRCS += commandline.cpp
CXXSRCS += console.cpp
CXXSRCS += fdevent.cpp
CXXSRCS += $(shell pwd)/sockets.cpp
CXXSRCS += file_sync_client.cpp
CXXSRCS += services.cpp
CXXSRCS += transport.cpp
CXXSRCS += transport_local.cpp
CXXSRCS += transport_usb.cpp
CXXSRCS += get_my_path_generic.cpp
CXXSRCS += usb_libusb.cpp

VPATH += ../libcutils
CSRCS += load_file.c
CSRCS += socket_inaddr_any_server.c
CSRCS += socket_local_client.c
CSRCS += socket_local_server.c
CSRCS += socket_loopback_client.c
CSRCS += socket_loopback_server.c
CSRCS += socket_network_client.c

VPATH += ../base
CXXSRCS += strings.cpp
CXXSRCS += stringprintf.cpp

CPPFLAGS += -DADB_REVISION=\"6.0.0_r1\"
CPPFLAGS += -DADB_HOST=1
CPPFLAGS += -I.
CPPFLAGS += -I../include
CPPFLAGS += -I../base/include
CPPFLAGS += $(shell pkg-config --cflags libusb-1.0)

CXXFLAGS += -std=gnu++11

LIBS += -lcrypto -lpthread -lz $(shell pkg-config --libs libusb-1.0)

OBJS=$(CSRCS:.c=.o)
OBJS+=$(CXXSRCS:.cpp=.o)

all: adb

adb: $(OBJS)
	$(CXX) -o $@ $(CPPFLAGS) $(CXXFLAGS) $(LDFLAGS) $(OBJS) $(LIBS)

clean:
	rm -f $(OBJS)
