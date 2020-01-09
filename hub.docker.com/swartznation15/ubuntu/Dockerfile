FROM ubuntu
LABEL edu.uanet.mds163-devops.url="https://github.com/bitshares/bitshares-core.git"
LABEL edu.uanet.mds163-devops.distro="ubuntu"
LABEL edu.uanet.mds163-devops.osversion="18.10"
LABEL edu.uanet.mds163-devops.architecture="x86_64"


RUN apt-get update -y && apt-get install -y \
make \
cmake \
g++ \
wget \
curl
CMD /bin/bash
RUN apt-get install -y wget


#pulling everything into the proper foramts to be used later
ARG SORT_VERSION=2.0.190219
#ARG SORT_VERSION=0.9.0
#ARG SORT_URL=https://github.com/mlcollard/sortDevOPS/archive/0.9.0.tar.gz
ARG SORT_URL=https://github.com/bitshares/bitshares-core/archive/2.0.190219.tar.gz

RUN curl -L -O $SORT_URL


RUN tar xvzf ${SORT_VERSION}.tar.gz
RUN ls
RUN cd bitshares-core-${SORT_VERSION}
RUN ls
RUN cmake 