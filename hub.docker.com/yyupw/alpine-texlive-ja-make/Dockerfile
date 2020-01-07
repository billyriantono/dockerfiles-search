FROM paperist/alpine-texlive-ja

MAINTAINER yyu <m [at] yyu.pw>

ENV PATH /usr/local/texlive/2016/bin/x86_64-linux:$PATH

RUN apk --no-cache add make

WORKDIR /workdir

VOLUME ["/workdir"]

CMD ["bash"]
