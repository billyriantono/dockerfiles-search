FROM ubuntu:16.04

# Install build dependencies (and vim + picocom for editing/debugging)
RUN apt-get -qq update \
    && apt-get install -y make unrar-free autoconf automake libtool libtool-bin \
       gcc g++ gperf flex bison texinfo gawk ncurses-dev libexpat-dev python-dev \
       python python-serial sed git unzip bash help2man wget bzip2 vim picocom \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Get the esp-open-sdk
RUN git clone --recursive https://github.com/pfalcon/esp-open-sdk.git /esp-open-sdk \
    && echo "CT_EXPERIMENTAL=y" >> /esp-open-sdk/crosstool-config-overrides \
    && echo "CT_ALLOW_BUILD_AS_ROOT=y" >> /esp-open-sdk/crosstool-config-overrides \
    && echo "CT_ALLOW_BUILD_AS_ROOT_SURE=y" >> /esp-open-sdk/crosstool-config-overrides

# Build the esp-open-sdk
# Clean out large and now unnecessary crosstool-NG build area
RUN cd /esp-open-sdk && make toolchain esptool libhal STANDALONE=n && \
 rm -fr /esp-open-sdk/crosstool-NG

# Add the esp-open-sdk bin folder to PATH
ENV PATH /esp-open-sdk/xtensa-lx106-elf/bin:$PATH

# Add ESP_OPEN_RTOS variable to point to path so that makefiles don't *have* to live in the
# examples directory (will require your makefile to reference $(ESP_OPEN_RTOS)/common.mk
ENV ESP_OPEN_RTOS=/esp-open-rtos

# Get the esp-open-rtos SDK
RUN git clone --recursive https://github.com/SuperHouse/esp-open-rtos.git $ESP_OPEN_RTOS
