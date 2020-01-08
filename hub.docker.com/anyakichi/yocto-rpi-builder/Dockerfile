ARG builder_base
FROM ${builder_base}

COPY extract.15.md /etc/buildenv.d/
COPY setup.15.md /etc/buildenv.d/

ARG yocto_machine
ENV \
  YOCTO_MACHINE=${yocto_machine}
