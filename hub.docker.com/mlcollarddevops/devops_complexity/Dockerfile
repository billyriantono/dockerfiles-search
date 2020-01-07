FROM fedora:rawhide
LABEL org.srcml.distro="fedora" \
      org.srcml.osversion="rawhide" \
      org.srcml.architecture="x86_64"

# Install dependencies
RUN dnf install -y \
    gcc-c++ \
    make \
    cmake \
    && dnf clean all
