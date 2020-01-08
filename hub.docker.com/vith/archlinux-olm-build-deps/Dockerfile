FROM archlinux/base

RUN pacman --noconfirm -Syu --needed base-devel emscripten perl-json cmake jre-openjdk-headless nodejs npm && \
    pacman --noconfirm -Scc

# cause /etc/profile.d/emscripten.sh to be sourced
# emcc prints an intro message the first time it runs instead of doing the build
RUN bash -l -c emcc 

# cause /etc/profile.d/emscripten.sh to be sourced
CMD ["/usr/bin/bash", "-l"]
