FROM fedora:29

ARG VERSION=v4.0-dev

LABEL maintainer="Stephen Legge <stephen@aleggeup.com>"

RUN dnf -y update
RUN dnf -y install git gcc python python3 python3-devel make cmake redhat-rpm-config bzip2 unzip ncurses ncurses-devel flex bison gperf python2-pyserial python2-cryptography python2-future python2-pyparsing

WORKDIR /esp
RUN git clone https://github.com/espressif/esp-idf.git

ENV IDF_TOOLS_PATH /esp/tools
WORKDIR /esp/esp-idf
RUN git submodule update --init --recursive
RUN ./install.sh

ENV PATH /esp/esp-idf/components/esptool_py/esptool:$PATH
ENV PATH /esp/esp-idf/components/espcoredump:$PATH
ENV PATH /esp/esp-idf/components/partition_table:$PATH
ENV PATH /esp/tools/tools/xtensa-esp32-elf/esp32-2019r1-8.2.0/xtensa-esp32-elf/bin:$PATH
ENV PATH /esp/tools/tools/esp32ulp-elf/2.28.51.20170517/esp32ulp-elf-binutils/bin:$PATH
ENV PATH /esp/tools/tools/openocd-esp32/v0.10.0-esp32-20190313/openocd-esp32/bin:$PATH
ENV PATH /esp/tools/python_env/idf4.0_py2.7_env/bin:$PATH
ENV PATH /esp/esp-idf/tools:$PATH

RUN useradd -ms /bin/bash esp32-builder
RUN groupmems --group dialout --add esp32-builder
RUN groupmems --group ftp --add esp32-builder

ADD ./skel/* /root/

USER esp32-builder
ADD ./skel/* /home/esp32-builder/
VOLUME /esp/project

WORKDIR /esp/project
ENTRYPOINT ["/bin/bash", "-i"]
