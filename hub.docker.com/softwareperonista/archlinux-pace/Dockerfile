# ArchLinux image with Pace dependencies

FROM archlinux/base:latest
MAINTAINER tarmaciltur

# Locale
RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Update and install needed packages
RUN pacman -Syu --noconfirm --noprogressbar base \ 
                                            base-devel \
                                            git \
                                            meson \
                                            vala \ 
                                            gtksourceview4 \
                                            appstream-glib \
                                            gettext \
                                            xorg-server-xvfb
 
# Clean cache
RUN pacman -Scc --noconfirm
