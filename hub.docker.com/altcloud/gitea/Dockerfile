FROM alt:p9

MAINTAINER alt-cloud

RUN apt-get update && \
    apt-get install -y gitea openssh-server; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

RUN apt-get update && \
    apt-get install -y gosu; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

ENV USER gitea
ENV HOME /var/lib/gitea
ENV GITEA_WORK_DIR /var/lib/gitea

WORKDIR /var/lib/gitea

COPY app.ini /etc/gitea/app.ini
COPY entrypoint.sh /entrypoint.sh

EXPOSE 3000
EXPOSE 2222

VOLUME ["/var/lib/gitea"]

ENTRYPOINT ["/entrypoint.sh"]
