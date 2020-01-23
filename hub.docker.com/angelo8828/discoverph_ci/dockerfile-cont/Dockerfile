FROM andzuc/gentoo-stage3amd64

ENV QEMU_VERSION="2.12.1"
COPY portage /etc/portage/
RUN emerge -v \
    --autounmask-write=y --autounmask-continue=y \
    =app-emulation/qemu-$QEMU_VERSION
