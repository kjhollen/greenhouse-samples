

UNAME_S := $(shell uname -s)
ifeq ($(UNAME_S),Darwin)
    CXX = clang++
endif

GH_PATH=/opt/oblong/greenhouse
DEPS_PATH=/opt/oblong/deps-64-8
GH_PKG_CONFIG=$(PKG_CONFIG_PATH):$(GH_PATH)/lib/pkgconfig $(DEPS_PATH)/bin/pkg-config

CXXFLAGS = -Wempty-body \
  -fdiagnostics-show-option \
  -Wall \
  -Wpointer-arith \
  -Wshadow \
  -Wwrite-strings \
  -Wno-overloaded-virtual \
  -Wno-strict-overflow \
  -Wno-error=unused-variable \
  -Werror \
  `PKG_CONFIG_PATH=$(GH_PKG_CONFIG) --cflags --static libGreenhouse` \
  -g -O3 -std=gnu++0x

LDFLAGS=`PKG_CONFIG_PATH=$(GH_PKG_CONFIG) --libs --static libGreenhouse`

NO_COLOR=\x1b[0m
OK_COLOR=\x1b[36;21m

define EXP_STR

======================================================================
TO HAVE YOUR APPLICATION FIND THE RESOURCES IN THE LOCAL SHARE FOLDER,
PLEASE RUN THE FOLLOWING:

export OB_SHARE_PATH=`pwd`/share:$$OB_SHARE_PATH

*Note: This will only affect your current terminal window.
======================================================================
endef
export EXP_STR

all: seismo
clean:
	-rm seismo

seismo: seismo.C
	${CXX} $^ -lGreenhouse ${LDFLAGS} ${CXXFLAGS} -o $@
	@echo	"$(OK_COLOR)$$EXP_STR$(NO_COLOR)"

