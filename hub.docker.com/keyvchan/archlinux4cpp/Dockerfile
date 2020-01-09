FROM archlinux/base:latest

#  Change source address

# Update package info
RUN pacman -Sy --noconfirm
RUN pacman -S git base-devel cmake gdb --noconfirm --needed 

# Create build user
RUN useradd -m builduser
RUN echo "builduser ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/notroot

USER builduser
WORKDIR /home/builduser

# Install trizen
RUN git clone https://aur.archlinux.org/trizen-git.git && cd trizen-git && makepkg --noconfirm -si

# Install vcpkg
RUN trizen -S vcpkg-git --noconfirm

USER root
WORKDIR /root/
# Install zsh and oh-my-zsh
RUN pacman -S zsh --noconfirm --needed && sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh) -y "

# Fix clang-format crash bug (May be fixed in newer version)
RUN ln -sf /usr/lib/libncursesw.so.6 /usr/lib/libtinfo.so.5

# Change shell to zsh
ENV SHELL=/usr/bin/zsh



