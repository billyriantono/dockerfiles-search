FROM archlinux/base

# Update system
RUN pacman -Syyu --noconfirm --noprogressbar

RUN pacman -S --noconfirm --noprogressbar \
    gcc \
    qt5-base \
    qt5-declarative \
    qt5-quickcontrols2 \
    qbs
    
# Clear pacman cache
RUN (echo -e "y\ny\n" | pacman -Scc | echo)

# Setup Qbs
RUN qbs-setup-toolchains --detect
RUN qbs-setup-qt /usr/bin/qmake default
RUN qbs config defaultProfile default
