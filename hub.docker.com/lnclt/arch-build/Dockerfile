FROM archlinux/base

# buildly custom config for pacman and makepkg
COPY ./pacman.conf /etc/pacman.conf
COPY ./makepkg.conf /etc/makepkg.conf

# Install base dependencies
RUN pacman -Syu --noconfirm base-devel wget sudo devtools

# Add builduser with passwordless sudo rights
RUN useradd builduser -m \
 && passwd -d builduser \
 && printf "builduser ALL=(ALL) ALL\n" | tee -a /etc/sudoers

# Prepare volumes
RUN mkdir -p /build/{pkg,repo} && chown -R builduser /build
WORKDIR "/build"

# Switch from root to builduser
USER builduser

# Install aurutils
RUN gpg --recv-key 6BC26A17B9B7018A \
 && wget "https://aur.archlinux.org/cgit/aur.git/snapshot/aurutils.tar.gz" \
 && tar -xf aurutils.tar.gz \
 && cd aurutils \
 && makepkg -sci --noconfirm
