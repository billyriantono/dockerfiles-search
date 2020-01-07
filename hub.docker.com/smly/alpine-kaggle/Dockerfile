FROM alpine:3.3

MAINTAINER Kohei <i@ho.lc>

# Ref: https://github.com/frol/docker-alpine-glibc
RUN ALPINE_GLIBC_BASE_URL="https://github.com/andyshinn/alpine-pkg-glibc/releases/download" && \
    ALPINE_GLIBC_PACKAGE_VERSION="2.23-r1" && \
    ALPINE_GLIBC_BASE_PACKAGE_FILENAME="glibc-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
    ALPINE_GLIBC_BIN_PACKAGE_FILENAME="glibc-bin-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
    ALPINE_GLIBC_I18N_PACKAGE_FILENAME="glibc-i18n-$ALPINE_GLIBC_PACKAGE_VERSION.apk" && \
    apk add --no-cache --virtual=build-dependencies wget ca-certificates && \
    wget \
        "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BASE_URL/$ALPINE_GLIBC_PACKAGE_VERSION/$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \
    apk add --no-cache --allow-untrusted \
        "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_I18N_PACKAGE_FILENAME" && \
    \
    /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true && \
    echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh && \
    \
    apk del glibc-i18n && \
    rm \
        "$ALPINE_GLIBC_BASE_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_BIN_PACKAGE_FILENAME" \
        "$ALPINE_GLIBC_I18N_PACKAGE_FILENAME"

# Miniconda + python packages
RUN MINICONDA_FILENAME="Miniconda2-3.19.0-Linux-x86_64.sh" && \
    MINICONDA_URL="https://repo.continuum.io/miniconda/$MINICONDA_FILENAME" && \
    apk add --no-cache libstdc++ && \
    apk add --no-cache --virtual=build-dependencies bash wget build-base musl-dev && \
    wget -q --no-check-certificate $MINICONDA_URL && \
    bash /$MINICONDA_FILENAME -b -p /opt/conda && \
    /opt/conda/bin/conda install -y scikit-learn numpy scipy pandas statsmodels && \
    /opt/conda/bin/pip install bloscpack awscli ml_metrics && \
    /opt/conda/bin/pip install blosc==1.2.5 && \
    \
    rm -rf /$MINICONDA_FILENAME /opt/conda/pkgs/*

# XGBoost
RUN XGBOOST_URL="https://github.com/dmlc/xgboost/archive/0.47.zip" && \
    XGBOOST_PATH="/opt/xgboost-0.47" && \
    XGBOOST_FILE="xgboost.zip" && \
    cd /opt && \
    wget -q --no-check-certificate $XGBOOST_URL -O $XGBOOST_FILE && \
    unzip $XGBOOST_FILE && rm $XGBOOST_FILE && cd $XGBOOST_PATH && \
    \
    make && \
    cd python-package && \
    /opt/conda/bin/python setup.py install
    # apk del build-dependencies


ENV PATH=/opt/xgboost-0.47:/opt/conda/bin:$PATH \
    LANG=C.UTF-8

CMD ["sh"]
