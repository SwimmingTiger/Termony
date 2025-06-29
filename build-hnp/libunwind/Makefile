all: download/libunwind-1.8.2.tar.gz
	rm -rf temp build
	mkdir -p temp build
	cd temp && tar xvf ../download/libunwind-1.8.2.tar.gz
	cd temp/libunwind-1.8.2 && PKG_CONFIG=/usr/bin/false LIBTOOL=glibtool LIBTOOLIZE=glibtoolize ./configure --host aarch64-unknown-linux-musl --enable-shared --disable-static --disable-udev CC=$(OHOS_SDK_HOME)/native/llvm/bin/aarch64-unknown-linux-ohos-clang LD=$(OHOS_SDK_HOME)/native/llvm/bin/ld.lld AR=$(OHOS_SDK_HOME)/native/llvm/bin/llvm-ar RANLIB=$(OHOS_SDK_HOME)/native/llvm/bin/llvm-ranlib STRIP=$(OHOS_SDK_HOME)/native/llvm/bin/llvm-strip
	cd temp/libunwind-1.8.2 && make -j $(shell nproc) && make install DESTDIR=$(shell pwd)/build
	mkdir -p ../sysroot
	rm -v build/usr/local/lib/*.la
	$(OHOS_SDK_HOME)/native/llvm/bin/llvm-strip build/usr/local/lib/*.so
	cp -rfv build/usr/local/. ../sysroot | tee file.lst

download/libunwind-1.8.2.tar.gz:
	mkdir -p download
	cd download && wget https://github.com/libunwind/libunwind/releases/download/v1.8.2/libunwind-1.8.2.tar.gz
