# YOSIS AND NEXTPNR
FROM johnnycubides/linux-nextpnr-ice40:nextpnr-ice40

WORKDIR /opt/

# LITEX
COPY --from=johnnycubides/linux-litex:litex /opt/migen /opt/migen
COPY --from=johnnycubides/linux-litex:litex /opt/litex /opt/litex
COPY --from=johnnycubides/linux-litex:litex /opt/liteeth /opt/liteeth
COPY --from=johnnycubides/linux-litex:litex /opt/litedram /opt/litedram
COPY --from=johnnycubides/linux-litex:litex /opt/litepcie /opt/litepcie
COPY --from=johnnycubides/linux-litex:litex /opt/litesata /opt/litesata
COPY --from=johnnycubides/linux-litex:litex /opt/litesdcard /opt/litesdcard
COPY --from=johnnycubides/linux-litex:litex /opt/liteiclink /opt/liteiclink
COPY --from=johnnycubides/linux-litex:litex /opt/litevideo /opt/litevideo
COPY --from=johnnycubides/linux-litex:litex /opt/litescope /opt/litescope
COPY --from=johnnycubides/linux-litex:litex /opt/litejesd204b /opt/litejesd204b
COPY --from=johnnycubides/linux-litex:litex /opt/litex-boards /opt/litex-boards
COPY --from=johnnycubides/linux-litex:litex /opt/litex_setup.py /opt/litex_setup.py

RUN python3 litex_setup.py install

### VERILATOR ###
RUN apt-get install -y verilator libevent-dev libjson-c-dev

# OPENOCD
COPY --from=johnnycubides/linux-openocd:openocd /opt/openocd /opt/openocd

RUN cd openocd && \
      make install

# LM32
COPY --from=johnnycubides/linux-lm32:lm32 /opt/lm32 /opt/lm32

RUN cd lm32 && \
      echo 'export PATH=/opt/lm32/bin/:$PATH' >> /root/.bashrc


