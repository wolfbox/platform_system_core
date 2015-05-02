HOST_OS := $(shell uname -s)

SRCS += adb.c
SRCS += adb_auth_host.c
SRCS += adb_client.c
SRCS += commandline.c
SRCS += console.c
SRCS += fdevent.c
SRCS += file_sync_client.c
SRCS += services.c
SRCS += sockets.c
SRCS += transport.c
SRCS += transport_local.c
SRCS += transport_usb.c
SRCS += usb_libusb.c
SRCS += usb_vendors.c

VPATH += ../libcutils
SRCS += load_file.c
SRCS += socket_inaddr_any_server.c
SRCS += socket_local_client.c
SRCS += socket_local_server.c
SRCS += socket_loopback_client.c
SRCS += socket_loopback_server.c
SRCS += socket_network_client.c

VPATH += ../libzipfile
SRCS += centraldir.c
SRCS += zipfile.c

ifeq (Linux,$(HOST_OS))
    SRCS += get_my_path_linux.c
else ifeq (Darwin,$(HOST_OS))
    SRCS += get_my_path_darwin.c
    LIBS += -framework CoreFoundation
else
    SRCS += get_my_path_generic.c
endif

CPPFLAGS += -DADB_HOST=1
CPPFLAGS += -DHAVE_FORKEXEC=1
CPPFLAGS += -DHAVE_OFF64_T=1
CPPFLAGS += -DHAVE_TERMIO_H
CPPFLAGS += -I.
CPPFLAGS += -I../include
CPPFLAGS += $(shell pkg-config --cflags libusb-1.0)

LIBS += -L/usr/local/lib
LIBS += -lcrypto -lpthread -lz $(shell pkg-config --libs libusb-1.0)

OBJS= $(SRCS:.c=.o)

all: adb

adb: $(OBJS)
	$(CC) -o $@ $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) $(OBJS) $(LIBS)

clean:
	rm -f $(OBJS)
