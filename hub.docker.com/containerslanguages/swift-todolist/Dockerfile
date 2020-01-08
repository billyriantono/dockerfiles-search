# To build it:
# docker build -t swift-todolist .

FROM swiftdocker/swift:snapshot-2016-09-02-a

MAINTAINER Mario Loriedo <mario.loriedo@gmail.com>

RUN apt-get update && \
    apt-get install -y libssl-dev libcurl4-openssl-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /src/

# The following block is a hack to avoid re-fetching 
# dependencies every time a source file is changed
COPY /Package.swift /Makefile /src/
RUN mkdir -p /src/Sources/Server && touch /src/Sources/Server/main.swift
RUN mkdir -p /src/Sources/SuperTodoList && touch /src/Sources/SuperTodoList/SuperTodoList.swift
RUN make refetch

COPY / /src/
RUN make build

EXPOSE 8090

CMD [".build/debug/Server"]
