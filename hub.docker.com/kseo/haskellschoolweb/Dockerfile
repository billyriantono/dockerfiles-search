FROM       haskell:8.0
MAINTAINER Kwang Yul Seo <kwangyul.seo@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends libicu-dev && \
    rm -rf /var/lib/apt/lists/*

ADD . /web
WORKDIR /web
RUN stack setup
RUN stack build

CMD ["stack", "exec", "haskellschoolweb"]
EXPOSE 3000
