FROM mpks/arch_dev_base:201910
MAINTAINER MPKSoft

# install radio packages
#############
RUN pacman -Sy extra/qwt --noconfirm
RUN pacman -U https://archive.archlinux.org/packages/g/gnuradio/gnuradio-3.7.13.4-5-x86_64.pkg.tar.xz --noconfirm

# map /data to host defined data path (used to store data from app)
VOLUME /data

# run 
CMD ["/bin/bash"]
