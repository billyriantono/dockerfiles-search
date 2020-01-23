# Build iPXE
FROM ubuntu:bionic AS ipxe_build

# Uncomment the files below to enable detailed logging
ARG  EFI_COMPILE_ARGS='DEBUG=dhcp,tftp,http,scsi,iscsi,aoe,bzimage,netdevice,snpnet,snponly,snp,efi_snp,efi_init,efi_pci,efi_driver,device,realtek,pci'
ARG KPXE_COMPILE_ARGS='DEBUG=dhcp,tftp,http,scsi,iscsi,aoe,bzimage,netdevice,snpnet,snponly,snp,efi_snp,efi_init,efi_pci,efi_driver,device,realtek,pci,undi,undiload,undinet'

# Install build dependencies
RUN apt-get update
RUN apt-get -y install git make gcc binutils perl mtools syslinux liblzma-dev genisoimage 

RUN git clone git://git.ipxe.org/ipxe.git
RUN cd /ipxe && git checkout master

# Turn off PIE - workaround for a bug in gcc
RUN sed -i 's/^CFLAGS.*/CFLAGS := -fno-pie/g' /ipxe/src/Makefile

# Enable menu and background images
RUN sed -i 's/.*CONSOLE_CMD.*/#define CONSOLE_CMD/g' /ipxe/src/config/general.h
RUN sed -i 's/.*IMAGE_PNG.*/#define IMAGE_PNG/g' /ipxe/src/config/general.h
RUN sed -i 's/.*CONSOLE_FRAMEBUFFER.*/#define CONSOLE_FRAMEBUFFER/g' /ipxe/src/config/console.h
# Enable imgverify and imgtrust
RUN sed -i 's/.*IMAGE_TRUST_CMD.*/#define IMAGE_TRUST_CMD/g' /ipxe/src/config/console.h
# HTTPS Disabled for time being because of incompatability with Windows HyperV as mentioned in https://forum.ipxe.org/showthread.php?tid=10998
# RUN sed -i 's/.*DOWNLOAD_PROTO_HTTPS.*/#define DOWNLOAD_PROTO_HTTPS/g' /ipxe/src/config/general.h

# Image formats
# RUN sed -i 's/.*IMAGE_NBI.*/#define IMAGE_NBI/g' /ipxe/src/config/general.h
# RUN sed -i 's/.*IMAGE_MULTIBOOT.*/#define IMAGE_MULTIBOOT/g' /ipxe/src/config/general.h
# RUN sed -i 's/.*IMAGE_COMBOOT.*/#define IMAGE_COMBOOT/g' /ipxe/src/config/general.h
# RUN sed -i 's/.*IMAGE_EFI.*/#define IMAGE_EFI/g' /ipxe/src/config/general.h
# RUN sed -i 's/.*IMAGE_PXE.*/#define IMAGE_PXE/g' /ipxe/src/config/general.h

RUN cd /ipxe/src && make bin-x86_64-efi/ipxe.efi ${EFI_COMPILE_ARGS}

# These image types only work with Legacy BIOS mode
# RUN sed -i 's/.*IMAGE_ELF.*/#define IMAGE_ELF/g' /ipxe/src/config/general.h
# RUN sed -i 's/.*IMAGE_BZIMAGE.*/#define IMAGE_BZIMAGE/g' /ipxe/src/config/general.h

RUN cd /ipxe/src && make bin-x86_64-pcbios/undionly.kpxe ${KPXE_COMPILE_ARGS}
RUN cd /ipxe/src && make bin-x86_64-pcbios/undionly.kkpxe ${KPXE_COMPILE_ARGS}

# Build target image
FROM alpine

RUN apk update && \
    apk upgrade && \
    apk add tftp-hpa --no-cache && \
    mkdir /data

COPY --from=ipxe_build /ipxe/src/bin-x86_64-pcbios/undionly.kpxe /data/undionly.kpxe
COPY --from=ipxe_build /ipxe/src/bin-x86_64-pcbios/undionly.kkpxe /data/undionly.kkpxe
COPY --from=ipxe_build /ipxe/src/bin-x86_64-efi/ipxe.efi /data/ipxe.efi

# Uncomment line below to add the official build of kpxe (without additional features)
ADD http://boot.ipxe.org/undionly.kpxe /data/undionly_original.kpxe

RUN chmod -R a+rX /data/*

EXPOSE 69/udp
EXPOSE 48000-49000/udp

ENTRYPOINT ["in.tftpd"]

CMD ["-L", "--verbose", "-u", "root", "--secure", "--create", "/data", "--port-range", "48000:49000"]