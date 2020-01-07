FROM eclipse/stack-base:ubuntu
RUN \
	sudo apt-get update \
	&& sudo apt-get install -y \
		make \
		binutils-arm-none-eabi \
		gcc-arm-none-eabi \
		gdb-arm-none-eabi \
		gdb gdbserver \
		libnewlib-arm-none-eabi \
		libstdc++-arm-none-eabi-newlib \
		openocd \
	&& sudo apt-get clean \
	&& sudo apt-get -y autoremove \
	&& sudo rm -rf /var/lib/apt/lists/*

