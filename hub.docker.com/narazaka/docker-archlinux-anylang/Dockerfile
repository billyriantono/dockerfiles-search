From base/archlinux:latest

# build tools for aur
RUN pacman -Sy && \
    pacman -S --noconfirm --needed base-devel git
# perl6
RUN useradd builduser --create-home -g users && \
    echo 'builduser ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers && \
    su builduser -c 'git clone https://aur.archlinux.org/moarvm.git /tmp/moarvm' && \
    cd /tmp/moarvm && \
    su builduser -c 'makepkg --noconfirm --skippgpcheck -si' && \
    cd && \
    rm -rf /tmp/moarvm && \
    su builduser -c 'git clone https://aur.archlinux.org/nqp.git /tmp/nqp' && \
    cd /tmp/nqp && \
    su builduser -c 'makepkg --noconfirm --skippgpcheck -si' && \
    cd && \
    rm -rf /tmp/nqp && \
    su builduser -c 'git clone https://aur.archlinux.org/rakudo.git /tmp/rakudo' && \
    cd /tmp/rakudo && \
    su builduser -c 'makepkg --noconfirm --skippgpcheck -si' && \
    cd && \
    rm -rf /tmp/rakudo
# other languages
RUN pacman -S --noconfirm --needed perl ruby nodejs
