# Pass "make S=1" on the make comamnd line to build a statically linked application
ifeq ($(S),1)
	STATIC = -static
else
	STATIC =
endif

#######################################################################
# Application Specific setup
#
# (Change as needed)
#######################################################################
app_name	:= hello
LIBS		:=
CFLAGS		:= -O2
SRC_FILES	:= hello.c


# Check that our build environtment is set up correctly
ifeq ("$(BUILDROOT_DIR)","")
BR_CHECK := $(error "The environment variable BUILDROOT_DIR has not been set.")
endif
ifeq ("$(SYSROOT_DIR)","")
SR_CHECK := $(error "The SYSROOT in the toolchain can not be detected")
endif
ifeq ("$(CROSS_COMPILE)","")
CC_CHECK := $(error "The CROSS_COMPILE prefix for the toolchain can not be detected")
endif
$(BR_CHECK)
$(SR_CHECK)
$(CC_CHECK)


# Manual setup if set_env.sh is not used
#TC_PATH=/home/renesas/toolchain/buildroot-2014.05/output/host/usr
#CROSS_COMPILE=arm-buildroot-linux-uclibcgnueabi-
ARCH:=arm

all: default

#default: br_check sr_check cc_check
default:
	$(CROSS_COMPILE)gcc $(STATIC) $(CFLAGS) --sysroot=$(SYSROOT_DIR) -o $(app_name) $(SRC_FILES) $(LIBS)

install:
	@# Copy to Buildroot overlay directory (only for Renesas BSP)
	cp $(app_name) $(BUILDROOT_DIR)/output/rootfs_overlay/root/bin
	@echo ''
	@echo 'Please run Buildroot again to repackage the rootfs image.'
	@echo 'For example:'
	@echo '  $$ cd $$BUILDROOT_DIR'
	@echo '  $$ make'

clean:
	@rm -f *.o
	@rm -f *.a
	@rm -f $(app_name)

