FROM ubuntu:latest
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y wget unzip
RUN wget https://download-chromium.appspot.com/dl/Linux_x64?type=snapshots
RUN unzip Linux_x64?type=snapshots
RUN apt-get install -y git
RUN git clone https://chromium.googlesource.com/chromium/tools/depot_tools.git
ENV PATH $PATH:/depot_tools
RUN mkdir chromium
RUN cd chromium
RUN apt-get install -y python
RUN fetch --no-history chromium
RUN cd src
RUN ./build/install-build-deps.sh
