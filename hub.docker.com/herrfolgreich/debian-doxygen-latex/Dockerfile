FROM debian

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      make doxygen doxygen-latex \
 && apt-get clean

VOLUME /app
WORKDIR /app
