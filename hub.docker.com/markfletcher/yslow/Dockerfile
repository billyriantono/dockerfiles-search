FROM markfletcher/phantomjs
MAINTAINER Mark Fletcher

RUN apt-get update \
  && apt-get install -y curl unzip \
  && curl -O "http://yslow.org/yslow-phantomjs-3.1.8.zip" \
  && unzip yslow-phantomjs-3.1.8.zip \
  && rm yslow-phantomjs-3.1.8.zip \
  && apt-get purge -y --auto-remove curl unzip

ENTRYPOINT ["phantomjs", "yslow.js", "--info", "grade", "--format", "tap", "--threshold", "'{\"overall\": \"B\", \"ycdn\": 65}'"]
