LIBNAME := ahocorasick
BUILD_DIRECTORY := build/
LIB_TARGET := $(BUILD_DIRECTORY)lib$(LIBNAME).so
HEADER_FILES := $(wildcard *.h)
OBJECT_FILES := $(addprefix $(BUILD_DIRECTORY),$(patsubst %.c,%.o,$(wildcard *.c)))
CFLAGS := -Wall
COMPILER := gcc
ifeq ($(PREFIX),)
    PREFIX := /usr
endif

.PHONY : clean install

all: $(LIB_TARGET)

$(LIB_TARGET): $(BUILD_DIRECTORY) $(OBJECT_FILES)
	$(COMPILER) --shared -o $(LIB_TARGET) $(OBJECT_FILES)

$(BUILD_DIRECTORY)%.o: %.c $(HEADER_FILES)
	$(COMPILER) -fPIC -o $@ -c $< $(CFLAGS)

$(BUILD_DIRECTORY):
	@mkdir -p $(BUILD_DIRECTORY)

install: $(LIB_TARGET)
	install -d $(DESTDIR)$(PREFIX)/lib/
	install -m 644 $(LIB_TARGET) $(DESTDIR)$(PREFIX)/lib/
	install -d $(DESTDIR)$(PREFIX)/include/
	install -m 644 ahocorasick.h $(DESTDIR)$(PREFIX)/include/
	install -m 644 replace.h $(DESTDIR)$(PREFIX)/include/
	install -m 644 actypes.h $(DESTDIR)$(PREFIX)/include/

clean:
	rm -rf $(LIB_TARGET) $(OBJECT_FILES)
