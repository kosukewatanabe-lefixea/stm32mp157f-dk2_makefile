#
# This Makefile copy from Distribution-Package/layers/meta-st/meta-st-stm32mp/recipes-extended/m4projects/files/Makefile.stm32
#
CC := $(CROSS_COMPILE)gcc
LD := $(CROSS_COMPILE)ld
AS := $(CROSS_COMPILE)ar
STRIP := $(CROSS_COMPILE)strip
OBJCOPY := $(CROSS_COMPILE)objcopy
SIZE := $(CROSS_COMPILE)size

ifeq ($(CPU_TYPE),M4)
COMMONFLAGS += -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16
endif
ifeq ($(CPU_TYPE),A7)
COMMONFLAGS += -mcpu=cortex-a7 -mthumb -mfloat-abi=hard -mfpu=neon-vfpv4
endif

LDSCRIPT = stm32mp15xx_m4.ld

# Project settings
PROJ_DIR  := .
PROJ_NAME := m4

# Output
OUT	  := $(PROJ_DIR)/out
BUILD_OUT := $(OUT)

# Bin
TESTELF := $(BUILD_OUT)/$(PROJ_NAME).elf
TESTBIN := $(BUILD_OUT)/$(PROJ_NAME).bin

# CFLAGS rules
CFLAGS	+= $(COMMONFLAGS)
CFLAGS	+= -Os
#CFLAGS	+= -Og
CFLAGS	+= -std=gnu11
CFLAGS	+= -fstack-usage
CFLAGS	+= -Wall -fmessage-length=0 -ffunction-sections -c -fmessage-length=0 -MMD -MP
#CFLAGS	+= -Wno-unused-function
#CFLAGS	+= -Wno-unused-variable
CFLAGS	+= -g3
#CFLAGS += -g
#CFLAGS += -Werror

# LDFLAGS rules
LDFLAGS	+= $(COMMONFLAGS)
LDFLAGS	+= -specs=nosys.specs -specs=nano.specs
LDFLAGS	+= -Wl,-Map=$(BUILD_OUT)/output.map -Wl,--gc-sections -lm
#LDFLAGS	+= -D__MEM_START__=0x2ffc2000 -D__MEM_END__=0x2fff3000 -D__MEM_SIZE__=0x31000
#debug LINKER
#LDFLAGS += -Wl,--verbose


# Get config code from the project to compile (source, cflags, ldflags, ldlibs)
# include $(BUILD_OUT)/conf/config.in

# Build rule
define c-compilation-rule
$1: $2 $(LDSCRIPT)
	@echo $2 \< $1
	@mkdir -pv `dirname $1`
	$(CC) $(CFLAGS) -c $2 -o $1
COBJ+=$1
endef

# generate a compilation rule for each source file
$(foreach r,$(CSRC), $(eval $(call c-compilation-rule,$(BUILD_OUT)/$(r).o,$(r))))

# Include dep files
#DEPS= $(foreach file,$(CSRC),$(file).d)
#-include $(DEPS)

# Build elf output
$(TESTELF): $(COBJ)
	@echo link $@
	$(CC)  $(LDFLAGS) -o $@.sym $^ $(LDLIBS) -T $(LDSCRIPT)
	@cp $@.sym $@
	@$(STRIP) -g $@
	@$(SIZE) $@

# Build bin output
$(TESTBIN): $(TESTELF)
	@$(OBJCOPY) -O binary $(TESTELF) $(TESTBIN)

clean:
	rm -rf $(COBJ) $(TESTELF) $(TESTBIN)

all: $(TESTBIN)



