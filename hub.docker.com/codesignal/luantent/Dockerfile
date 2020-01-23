FROM ruby:latest

# Install build tools:
RUN apt-get update -qq && apt-get install -y build-essential autoconf libtool

# Download and make gRPC:
ENV GRPC_PATH=/tmp/grpc
RUN git clone --depth 1 https://github.com/grpc/grpc.git $GRPC_PATH
WORKDIR $GRPC_PATH
RUN git submodule update --init
RUN make

# Before we install gRPC we need to install protobuf v3 library. Thankfully this
# comes bundled with the gRPC library we already installed.
WORKDIR third_party/protobuf
RUN make install

# Eventually we can install gRPC itself.
WORKDIR $GRPC_PATH
RUN make install

# Clean up after the installation.
WORKDIR /
RUN rm -rf $GRPC_PATH
