FROM ubuntu:bionic

RUN apt update \
&&  apt install -y gdb \
&&  apt clean

COPY inputrc /root/.inputrc
COPY gdbinit /root/.gdbinit
COPY entrypoint /entrypoint
RUN chmod 555 /entrypoint

ENTRYPOINT ["/entrypoint"]

# Default empty command, processing is handled by entrypoint
CMD []
