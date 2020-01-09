FROM phusion/baseimage
MAINTAINER Alejandro Barrera <alejandro.barrera@duke.edu>

# Install dependencies
RUN apt-get update && apt-get install -y \
  libgsl2 \
  libgsl0-dev \
  curl \
  lbzip2

# Download pre-compiled preseq into /opt/
ENV PRESEQ_RELEASE=2.0
ENV PRESEQ_URL=http://smithlabresearch.org/downloads/preseq_linux_v${PRESEQ_RELEASE}.tar.bz2
ENV DEST_DIR=/opt/

# Softlink the scientific GNU library shared object
RUN ln -s /usr/lib/x86_64-linux-gnu/libgsl.so /usr/lib/x86_64-linux-gnu/libgsl.so.0

# Download preseq; untar & decompress; remove tr.bz2 file
RUN curl -SLo ${DEST_DIR}/preseq_v${PRESEQ_RELEASE}.tar.bz2 ${PRESEQ_URL} && \
  tar -xf ${DEST_DIR}/preseq_v${PRESEQ_RELEASE}.tar.bz2 -C ${DEST_DIR} && \
  rm -f ${DEST_DIR}/preseq_v${PRESEQ_RELEASE}.tar.bz2

# Add preseq to the PATH
ENV PATH=${DEST_DIR}/preseq_v${PRESEQ_RELEASE}:$PATH


CMD ["preseq"]
