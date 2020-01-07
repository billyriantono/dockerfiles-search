FROM golang:1.10

ENV GLIDE_VERSION v0.13.1

# Install glide
WORKDIR $GOPATH/src/github.com/Masterminds
RUN git clone https://github.com/Masterminds/glide.git
RUN cd glide && git checkout $GLIDE_VERSION && make bootstrap-dist && make install
WORKDIR $GOPATH
