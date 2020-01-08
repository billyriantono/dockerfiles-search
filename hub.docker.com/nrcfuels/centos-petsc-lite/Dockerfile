# Set an empty SDE, scripts should detect and populate with
# the last commit date or current unix epoch.
ARG SOURCE_DATE_EPOCH=

# Define a image to build gcc to avoid having to
# do a bootstrap build
FROM nrcfuels/centos-mpich-lite:latest

ARG SOURCE_DATE_EPOCH

ENV PACKAGES_DIR /opt
ENV PETSC_VER 3.9.4
ENV GCC_VER ${GCC_VER:-8.2.0}
ENV PETSC_PREFIX ${PACKAGES_DIR}/petsc-${PETSC_VER}/gcc-${GCC_VER}
ENV PKG_SRC /tmp/pkg_source

WORKDIR ${PKG_SRC}

COPY ./scripts/petsc-${PETSC_VER}.tar.gz.sha256 \
     ./scripts/install-petsc.sh ./
RUN ./install-petsc.sh && rm ./install-petsc.sh
ENV PATH ${PETSC_PREFIX}/bin:${PATH}
ENV PETSC_DIR=${PETSC_PREFIX}

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VCS_URL
ARG VCS_VERSION=latest
LABEL org.label-schema.schema-version="1.0" \
      org.label-schema.build-date="$BUILD_DATE" \
      org.label-schema.version="$VCS_VERSION" \
      org.label-schema.name="centos-petsc-lite" \
      org.lavel-schema.source-date-epoch="$SOURCE_DATE_EPOCH" \
      org.label-schema.description="CentOS 7 base image w/ gcc, git, CMake, MPICH, and PETSC" \
      org.label-schema.url="https://github.com/nrc-fuels/centos-petsc-lite/" \
      org.label-schema.vcs-ref="$VCS_REF" \
      org.label-schema.vcs-url="$VCS_URL" \
      org.label-schema.vendor="nrcfuels" \
      org.label-schema.license="N/A" \
      org.label-schema.docker.cmd="docker run -v $(pwd):/workdir -i -t nrcfuels/centos-petsc-lite:latest"
