FROM java:openjdk-8-jre

MAINTAINER TsungKang <tsungkang@163.com>
ARG VERSION=0.8.1

# do all in one step
RUN mkdir /cerebro && \
    cd /cerebro && \
    curl -sSL https://github.com/lmenezes/cerebro/releases/download/v${VERSION}/cerebro-${VERSION}.tgz | tar xz --strip 1
WORKDIR /cerebro
EXPOSE 9000
CMD bin/cerebro