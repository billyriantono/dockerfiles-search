FROM fedora:latest

ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8

#
# Fix for running on older kernels
#
# dnf install binutils
# strip -R .note.ABI-tag /lib64/libQt5Core.so.5.11.3
#
# More info: https://github.com/Microsoft/WSL/issues/3023
#

RUN dnf -y install \
  binutils \
  dos2unix \
  doxygen \
  findutils \
  git \
  libxslt \
  make \
  pandoc \
  python3-docutils \
  python3-sphinx \
  python3-sphinx_rtd_theme \
  latexmk \
  rsync \
  texlive-latex \
  texlive-collection-latexrecommended \
  texlive-collection-latexextra \
  texlive-collection-fontsrecommended \
  texlive-collection-fontsextra \
  texlive-ec \
  texlive-cm-super \
  unzip \
  wkhtmltopdf \
  xz \
  zip \
 && dnf clean all

RUN ln -s /usr/bin/sphinx-build-3 /usr/bin/sphinx-build

RUN strip -R .note.ABI-tag /lib64/libQt5Core.so.5

