FROM yotoplay/esp-idf-builder:latest

# Install build dependencies (and vim + picocom for editing/debugging)
RUN apt-get -y -qq update \
    && apt -y upgrade \
    && apt-get install -y libglib2.0-dev libfdt-dev libpixman-1-dev zlib1g-dev \
                          python3-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Environment variables
ENV PATH="${PATH}:${ESP_TCHAIN_BASEDIR}:${ESP_TCHAIN_BASEDIR}/xtensa-esp32-elf/bin:${IDF_PATH}/tools:${ESP_TCHAIN_BASEDIR}/fwscripts:/qemu_esp32/xtensa-softmmu/"

RUN cd / \
    && wget -O /qemu_support.tar.gz https://www.dropbox.com/s/6t4aqw1iu1x63uv/qemu_support.tar.gz?dl=1 \ 
    && tar -xzf /qemu_support.tar.gz \
    && mkdir -p /esp/qemu \
    && cp /qemu_support/rom*bin /esp/qemu/ \
    && mv /qemu_support/qemu_esp32 / \
    && rm -rf /qemu_support /qemu_support.tar.gz

# Set default python to 2.7, required for idf/esp
RUN cd /usr/local/bin
RUN ln -s /usr/bin/python2.7 python
RUN pip install --user -r $IDF_PATH/requirements.txt

# This is the directory where our project will show up
WORKDIR ${ESP_TCHAIN_BASEDIR}/project
ENTRYPOINT ["idf.py"]
