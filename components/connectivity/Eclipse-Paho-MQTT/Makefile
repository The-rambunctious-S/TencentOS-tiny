###################################################################
#automatic detection QTOP and LOCALDIR
CUR_DIR := $(realpath $(dir $(realpath $(firstword $(MAKEFILE_LIST)))))
TRYQTOP := $(shell if [ -n "$$QTOP" ] ; then\
        echo $$QTOP;\
        else\
        cd $(CUR_DIR); while /usr/bin/test ! -d qmk ; do \
        dir=`cd ../;pwd`;                       \
        if [ "$$dir" = "/" ] ; then             \
           echo Cannot find QTOP in $(firstword $(MAKEFILE_LIST)) 1>&2; \
           exit 1;                              \
        fi ;                                    \
        cd $$dir;                               \
        done ;                                  \
        pwd;                                    \
        fi)
QTOP ?= $(realpath ${TRYQTOP})

ifeq ($(QTOP),)
$(error Please run this in a tree)
endif
LOCALDIR = $(patsubst %/,%,$(subst $(realpath $(QTOP))/,,$(CUR_DIR)))

####################################################################


TREE_LIB_ENABLE=1
lib=
subdirs=

CFGFLAGS += -I$(CUR_DIR)/3rdparty/include 
CFGFLAGS += -I$(CUR_DIR)/wrapper/include 
CFGFLAGS += -I$(QTOP)/net/sal_module_wrapper

LSRCS_DIR   += 3rdparty/src 
LSRCS_DIR   += wrapper/src



include ${QTOP}/qmk/generic/Make.tpl


