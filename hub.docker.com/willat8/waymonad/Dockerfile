FROM haskell:8.6.3 as builder

RUN sed -i 's/stretch /buster /' /etc/apt/sources.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    libgbm-dev \
    libpixman-1-dev \
    libegl1-mesa-dev \
    libgles2-mesa-dev \
    libinput-dev \
    libfuse-dev \
    cmake \
    wayland-protocols \
    libxkbcommon-dev \
    libxcb-composite0-dev \
    libxcb-image0-dev \
    gcc

RUN pip3 install meson ninja
RUN git clone --depth 1 https://git.kernel.org/pub/scm/linux/kernel/git/morgan/libcap.git \
 && git clone https://github.com/willat8/wlroots.git \
 && git clone --recursive --depth 1 https://github.com/willat8/waymonad-config.git  # redo23

WORKDIR /libcap

RUN make \
 && make lib=lib install \
 && make prefix=/libcap_install install

WORKDIR /wlroots

RUN git checkout waymonad \
 && meson build --prefix=/wlroots_install -Dx11-backend=disabled \
 && ninja -C build \
 && ninja -C build install \
 && cp -r /wlroots_install/* /usr  # Is there a better way to do this?

WORKDIR /waymonad-config

RUN cabal new-update \
 && cabal new-build

FROM debian:sid

COPY group passwd shadow /etc/

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    libc-bin \
    libwayland-cursor0 \
    libwayland-egl1 \
    libfuse2 \
    libinput10 \
    libpixman-1-0 \
    libxcb-composite0 \
    libxcb-render0 \
    libxkbcommon0 \
    libegl1 \
    libgles2 \
    libgl1-mesa-dri \
    weston \
    sudo \
    firefox \
 && rm -rf /var/lib/apt/lists/* # redo3

COPY --from=builder /libcap_install /wlroots_install /usr/
COPY --from=builder /waymonad-config/dist-newstyle/build/x86_64-linux/ghc-8.6.3/waymonad-config-0.0.1.0/x/waymonad-my/build/waymonad-my/waymonad-my /usr/bin

# agetty can only be run as root, also allows us to set capabilities
RUN chmod +s /sbin/agetty

# Temporary, can be removed when mounting home directory
RUN install -d -o will -g users /home/will

USER will
ENV XDG_RUNTIME_DIR=/tmp
WORKDIR /home/will

ENTRYPOINT exec agetty --login-options "--caps=cap_sys_admin,cap_setpcap,cap_setuid,cap_setgid+ep --inh=cap_sys_admin --keep=1 --user=$(id -un) --addamb=cap_sys_admin -- -c $0 $@" --autologin "$(id -un)" --login-program /usr/sbin/capsh --noclear tty$XDG_VTNR

CMD ["/usr/bin/waymonad-my"]

