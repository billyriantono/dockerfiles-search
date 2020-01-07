### 0x666f6f/alpine-datascience:base-miniconda
#
# Docker image using Alpine Linux with frolvlad/alpine-miniconda3 (frolvlad/alpine-glibc:alpine-3.9, miniconda);
#   plus standard data science libraries (Jupyter, Numpy, Pandas, SciPy and Seaborn/Matplotlib).
#   NB: This image is intended to emulate 0x666f6f/alpine-datascience:base using the Miniconda as the base. This image is 1.43GB (versus 541MB).
#
# Execute with: `docker run --rm -v ${HOME}:/mnt -p 8888:8888 0x666f6f/alpine-datascience:base-miniconda`

FROM frolvlad/alpine-miniconda3:python3.7  

########################################################################
# Set up OS
########################################################################

EXPOSE 8888
WORKDIR /mnt

ENV CPPFLAGS=-s \
    SHELL=/bin/bash

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["jupyter-notebook", "--JupyterApp.ip=0.0.0.0", "--JupyterApp.token=''", "--JupyterApp.password=''", "--allow-root"]

RUN conda config --add channels defaults \
  && conda config --add channels bioconda \
  && conda config --add channels conda-forge \
\
# CORE PACKAGES
  && apk --no-cache add bash \
      curl \
      tini \
      wget \
\
# PATCHES
  && echo "### Alpine compatibility patch for various packages" && \
    if [ ! -f /usr/include/xlocale.h ]; then \
      if [ ! -d /usr/include ]; then mkdir /usr/include; fi; \
      echo '#include <locale.h>' > /usr/include/xlocale.h; \
    fi \
\
########################################################################
# Install Python3, Jupyter
########################################################################
\
#  && conda install conda-build \
  && conda update -n base -c defaults conda \
  && conda install python=3.7 jupyter numpy pandas scipy seaborn \
  && conda update --all && conda clean -ya \
\
\
# CLEANUP
  && echo "### Cleanup unneeded files" \
  && rm -rf /tmp/build  ~/.cache/pip/*  \
  && strip --strip-unneeded --strip-debug /usr/lib/*.a || true \
  && find /usr/share/terminfo -type f -delete
