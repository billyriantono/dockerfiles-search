#*****************************************************************************
#   Dockerfile for texlive based on Fedora
#   Created on Fri 19 Oct 2018 16:49:12 BST
#   Copyright 2018 by Till Hofmann <hofmann@kbsg.rwth-aachen.de>
#*****************************************************************************
#
#   Distributed under terms of the MIT license.
#
#*****************************************************************************

FROM fedora:rawhide
ENV TEX_VERSION=2019
RUN dnf -y --nodocs install \
      file \
      git \
      grep \
      latexmk \
      make \
      openssh-clients \
      texlive-scheme-full \
    && dnf clean all
# Check that we actually installed the expected version of texlive
RUN bash -c '\
    tv=$(tex --version | grep -o "(TeX Live [0-9]*)" | grep -o "[0-9]*"); \
    if [ "$tv" != "$TEX_VERSION" ] ; then \
      echo "Unexpected TeX version $tv, expected TeX version $TEX_VERSION"; exit 1; \
    fi'
