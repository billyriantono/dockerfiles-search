FROM hoertech/docker-buildenv:mha_x86_64-linux-gcc-7
USER root
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get -y install netpbm fig2dev doxygen graphviz texlive \
                       texlive-latex-extra texlive-font-utils
USER u
