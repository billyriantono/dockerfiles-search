FROM alt:p9

MAINTAINER alt-cloud

RUN apt-get update && \
    apt-get install -y irb; \
    rm -f /var/cache/apt/archives/*.rpm \
          /var/cache/apt/*.bin \
          /var/lib/apt/lists/*.*

CMD ["irb"]
