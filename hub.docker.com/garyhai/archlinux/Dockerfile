FROM base/archlinux

MAINTAINER Gary Hai "gary@XL59.com"

# This Shouldent be Needed for :Latest But Just to Be Sure
RUN pacman-key --init
RUN pacman-key --populate archlinux

# Now Lets Update
RUN pacman -Syu --noconfirm --ignore filesystem
