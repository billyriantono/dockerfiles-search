FROM swift:4.2

RUN apt-get update && apt-get install -y \
	build-essential \
	libserd-dev \
	libsqlite3-dev \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir /work
WORKDIR /work

RUN mkdir -p /data/default
RUN mkdir -p /data/named

COPY Package.swift .
COPY Sources Sources
RUN swift build
COPY entrypoint.sh entrypoint.sh

RUN mkdir /endpoint

EXPOSE 8080
VOLUME ["/data"]
ENV PATH="/work:/work/.build/debug:${PATH}"

ENTRYPOINT ["kineo-endpoint"]
CMD ["-D", "/data"]
