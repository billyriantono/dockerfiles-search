############################################################
# Dockerfile
############################################################

# Set the base image
FROM docker.io/fedora:30

############################################################
# Configuration
############################################################
ENV VERSION "1.9.2"
ENV BUILDAH_ISOLATION=chroot

############################################################
# Installation
############################################################

RUN dnf -y install \
    # Build Dependencies
    make \
    golang \
    bats \
    btrfs-progs-devel \
    device-mapper-devel \
    glib2-devel \
    gpgme-devel \
    libassuan-devel \
    libseccomp-devel \
    ostree-devel \
    git \
    bzip2 \
    go-md2man \
    # Runtime Dependencies
    fuse-overlayfs \
    runc \
    containers-common &&\
    # Clone Repository
    mkdir -p ~/buildah /buildah/src/github.com/containers/buildah &&\
    export GOPATH=~/buildah &&\
    git clone https://github.com/containers/buildah.git ~/buildah/src/github.com/containers/buildah &&\
    cd ~/buildah/src/github.com/containers/buildah &&\
    git checkout tags/v${VERSION} &&\
    # Build Binary
    make &&\
    sudo make install &&\
    # Configuration
    sed -i 's/driver = "overlay"/driver = "vfs"/g' /etc/containers/storage.conf &&\
    sed -i 's/mountopt = "nodev,metacopy=on"/# mountopt = "nodev,metacopy=on"/g' /etc/containers/storage.conf &&\
    # CleanUp
    rm -rf ~/buildah &&\
    rm -rf /var/cache/dnf &&\
    dnf remove -y git bzip2 go-md2man

############################################################
# Execution
############################################################
CMD ["buildah", "--help"]
