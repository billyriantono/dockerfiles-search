FROM ubuntu:16.04

RUN apt-get update && apt-get install -y zip unzip libxt-dev wget libjasper-runtime
RUN mkdir /tmp/mcr_installer && \
    cd /tmp/mcr_installer && \
    wget http://ssd.mathworks.com/supportfiles/downloads/R2016b/deployment_files/R2016b/installers/glnxa64/MCR_R2016b_glnxa64_installer.zip && \
    unzip MCR_R2016b_glnxa64_installer.zip && \
    ./install -mode silent -agreeToLicense yes && \
    rm -Rf /tmp/mcr_installer
ENV MCRROOT=/usr/local/MATLAB/MATLAB_Runtime/v91 MCR_CACHE_ROOT=/tmp
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$MCRROOT/runtime/glnxa64:$MCRROOT/bin/glnxa64:$MCRROOT/sys/os/glnxa64:$MCRROOT/sys/opengl/lib/glnxa64:$MCRROOT/sys/java/jre/glnxa64/jre/lib/amd64/native_threads:$MCRROOT/sys/java/jre/glnxa64/jre/lib/amd64/server:$MCRROOT/sys/java/jre/glnxa64/jre/lib/amd64
