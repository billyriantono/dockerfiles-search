FROM samloh84/centos:7

ARG PRODUCT=ruby
ARG PRODUCT_VERSION=2.4.1
ARG TEMP_DIR_ROOT=/tmp/${PRODUCT}
ARG TEMP_DIR=/${TEMP_DIR_ROOT}/${PRODUCT_VERSION}
ARG INSTALL_DIR_ROOT=/opt/${PRODUCT}
ARG INSTALL_DIR=${INSTALL_DIR_ROOT}/${PRODUCT_VERSION}

ARG RUBY_SRC_TARGZ_URL="https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.1.tar.gz"
ARG RUBY_SRC_TARGZ=ruby-2.4.1.tar.gz
ARG RUBY_SRC_TARGZ_SHA256SUM=a330e10d5cb5e53b3a0078326c5731888bb55e32c4abfeb27d9e7f8e5d000250

USER ${ROOT_UID}

RUN \
RUBY_COMPILE_DEPENDENCIES="gcc gcc-c++ make zlib-devel gdbm-devel openssl-devel readline-devel" && \
yum-install ${RUBY_COMPILE_DEPENDENCIES} && \
mkdir -p ${TEMP_DIR} ${INSTALL_DIR} && \
pushd ${TEMP_DIR} && \
curl -LjSs \
${RUBY_SRC_TARGZ_URL} -o ${RUBY_SRC_TARGZ} && \
echo "${RUBY_SRC_TARGZ_SHA256SUM}  ${RUBY_SRC_TARGZ}" | sha256sum -c - && \
tar -xf ${RUBY_SRC_TARGZ} --strip-components=1 -C ${TEMP_DIR} && \
./configure --prefix=${INSTALL_DIR} && \
make && \
make install && \
pushd ${INSTALL_DIR} && \
PATH=${PATH}:${INSTALL_DIR}/bin gem update --system && \
popd && \
fix-ownership ${INSTALL_DIR} && \
fix-permissions ${INSTALL_DIR} && \
yum remove -y ${RUBY_COMPILE_DEPENDENCIES} && \
yum clean all && \
popd && \
rm -rf ${TEMP_DIR_ROOT}

ENV RUBY_HOME ${INSTALL_DIR}
ENV PATH ${RUBY_HOME}/bin:${PATH}

USER ${APP_UID}
