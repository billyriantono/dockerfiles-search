FROM arnow117/ubuntu_base:latest

MAINTAINER arnow117 "arnow117@gmail.com"
ENV TOOLS_PATH /root/Tools
ENV WORK_PATH /root/Workspace

# install unicorn engine
WORKDIR $TOOLS_PATH
ENV UNICORN_VER 1.0.1
RUN apt-get update -y && apt-get install -y python-dev libglib2.0-dev wget less vim
RUN wget https://codeload.github.com/unicorn-engine/unicorn/tar.gz/$UNICORN_VER && tar -xzf $UNICORN_VER
RUN rm $UNICORN_VER
WORKDIR $TOOLS_PATH/unicorn-$UNICORN_VER
RUN ./make.sh && ./make.sh install
WORKDIR $TOOLS_PATH/unicorn-$UNICORN_VER/bindings/python
RUN make install
RUN make install3

# install binwalk
WORKDIR $TOOLS_PATH
RUN git clone https://github.com/devttys0/binwalk.git && \
	cd binwalk && \
	./deps.sh --yes && \
    python3 setup.py install

# install radrare2
WORKDIR $TOOLS_PATH
RUN git clone https://github.com/radare/radare2.git && \
  cd radare2 && \
  ./sys/install.sh && \
  make install

WORKDIR $WORK_PATH