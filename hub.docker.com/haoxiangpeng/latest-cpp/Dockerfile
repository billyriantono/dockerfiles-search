FROM archlinux/base

LABEL maintainer="Xiangpeng Hao <haoxiangpeng@hotmail.com>"

RUN echo "Server = https://mirrors.ocf.berkeley.edu/archlinux/\$repo/os/\$arch" > /etc/pacman.d/mirrorlist \
  && pacman -Syy \
  && pacman -S numactl awk make pkg-config gcc clang cmake ndctl extra/openmp git --noconfirm \
  && git clone https://github.com/pmem/pmdk.git \
  && cd pmdk \
  && make -j \
  && make install

ENTRYPOINT [ "/usr/bin/g++" ]

