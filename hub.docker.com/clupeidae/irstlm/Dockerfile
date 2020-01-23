FROM ubuntu:18.04 as builder

LABEL author="Mirko Hering <mirko@jmhering.net>" \
      org.label-schema.name="IRSTLM" \
      org.label-schema.vcs-url="https://github.com/clu-pei-dae/docker-irstlm"

RUN apt-get update \
    && apt-get install -y build-essential git cmake libtool libc-dev gcc zlib1g-dev sphinxbase-utils\
    && rm -rf /var/lib/apt/lists/*

RUN mkdir /build/ /opt/irstlm \
    && cd /build \
    && git clone https://github.com/irstlm-team/irstlm.git irstlm \
    && cd irstlm \
    && CXXFLAGS=-isystem\ /usr/include/c++/7/ cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX=/opt/irstlm \
    && make \
    && make install \
    && ls -alR /opt/irstlm

FROM ubuntu:18.04 as irstlm

LABEL author="Mirko Hering <mirko@jmhering.net>"

RUN apt-get update \
    && apt-get install -y libtool zlib1g\
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /opt/irstlm /opt/irstlm

ENV IRSTLM "/opt/irstlm"

CMD [ "/opt/irstlm/bin/wrapper" ]
