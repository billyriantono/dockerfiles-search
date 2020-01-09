FROM ubuntu:18.04

# Install build dependencies (and vim + picocom for editing/debugging)
RUN apt-get -qq update \
    && apt-get install -y gcc git wget make libncurses-dev flex bison gperf python python-serial python-pip \
                          cmake ninja-build ccache vim picocom \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Get the ESP32 toolchain
ENV ESP_TCHAIN_BASEDIR /opt/local/espressif

RUN mkdir -p $ESP_TCHAIN_BASEDIR && wget -q -O- https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz | tar -xz -C $ESP_TCHAIN_BASEDIR/
RUN mkdir -p $ESP_TCHAIN_BASEDIR && wget -q -O- https://dl.espressif.com/dl/esp32ulp-elf-binutils-linux64-d2ae637d.tar.gz | tar -xz -C $ESP_TCHAIN_BASEDIR/

# Setup IDF_PATH
RUN mkdir -p /esp && cd /esp && git clone --recursive https://github.com/espressif/esp-idf.git
ENV IDF_PATH /esp/esp-idf

# Install python dependencies
RUN /usr/bin/python -m pip install --user -r /esp/esp-idf/requirements.txt

# Force the use of ccache
RUN mkdir -p /opt/ccache/bin && for prog in /opt/local/espressif/*/bin/*; do ln -s /usr/bin/ccache /opt/ccache/bin/$(basename $prog); done

# Add the toolchain binaries to PATH
ENV PATH /opt/ccache/bin:$ESP_TCHAIN_BASEDIR/xtensa-esp32-elf/bin:$ESP_TCHAIN_BASEDIR/esp32ulp-elf-binutils/bin:$IDF_PATH/tools:$PATH

# This is the directory where our project will show up
RUN mkdir -p /esp/project
WORKDIR /esp/project
ENTRYPOINT ["/bin/bash"]
