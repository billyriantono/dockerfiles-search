FROM python:2

RUN pip install grpcio --ignore-installed && \
    pip install grpcio-tools && \
    apt update -y && \
    apt install -y build-essential autoconf libtool pkg-config && \
    apt install -y libgflags-dev libgtest-dev && \
    git clone https://github.com/grpc/grpc.git && \
    cd grpc && \
	git submodule update --init && \
    make grpc_cli && \
	cp /grpc/bins/opt/grpc_cli /usr/local/bin/ && \
	cd ../ && rm -rf grpc

ENTRYPOINT ["/usr/local/bin/grpc_cli"]
