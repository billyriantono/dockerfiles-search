FROM ubuntu:18.04 as xgboost

WORKDIR /

RUN  \
    apt update \
    && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        ca-certificates \
        zip \
    && update-ca-certificates \
    && git clone --recursive https://github.com/dmlc/xgboost \
    && cd xgboost \
    && mkdir build \
    && cd build \
    && cmake .. \
    && make -j4



FROM ubuntu:18.04

WORKDIR /
COPY --from=xgboost /xgboost/lib/libxgboost.so /usr/local/lib/
ARG WEKA_VER=weka-3-9-3

RUN \
    apt update \
    && apt install -y --no-install-recommends \
        ca-certificates \
        default-jre \
        libgomp1 \
        wget \
        unzip \
    \
    && wget https://nchc.dl.sourceforge.net/project/weka/weka-3-9/3.9.3/${WEKA_VER}.zip \
    && unzip ${WEKA_VER}.zip \
    && ln -s ${WEKA_VER} weka \
    && mkdir -p /root/wekafiles/systemDialogs \
    && touch /root/wekafiles/systemDialogs/weka.gui.GUIChooser.HowToFindPackageManager \
    && ln -s /weka /root/ \
    && rm ${WEKA_VER}.zip \
    \
    && wget https://jaist.dl.sourceforge.net/project/weka/datasets/datasets-numeric/datasets-numeric.jar \
    && unzip datasets-numeric.jar -d /weka/data/ \
    && rm datasets-numeric.jar \
    \
    && wget https://github.com/SigDelta/weka-xgboost/releases/download/0.1.0/xgboost-0.1.0.zip \
    && java -cp /weka/weka.jar weka.core.WekaPackageManager -install-package xgboost-0.1.0.zip \
    && rm xgboost-0.1.0.zip \
    \
    && wget https://github.com/Waikato/wekaDeeplearning4j/releases/download/v1.5.13/wekaDeeplearning4j-1.5.13.zip \
    && java -cp /weka/weka.jar weka.core.WekaPackageManager -install-package wekaDeeplearning4j-1.5.13.zip \
    && rm wekaDeeplearning4j-1.5.13.zip

WORKDIR /weka
ENTRYPOINT [ "/usr/bin/java", "-jar", "/weka/weka.jar" ]
