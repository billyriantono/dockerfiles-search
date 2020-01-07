FROM haskell:8 AS build

RUN apt-get update \
  && apt-get install -y --fix-missing --no-install-recommends \
    libpcre3 \
    libpcre3-dev \
    build-essential \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG DUCKLING_VERSION

RUN git clone --branch $DUCKLING_VERSION --depth 1 https://github.com/facebook/duckling.git

RUN mkdir /log

WORKDIR /duckling

RUN stack setup
# NOTE:`stack build` will use as many cores as are available to build
# in parallel. However, this can cause OOM issues as the linking step
# in GHC can be expensive. If the build fails, try specifying the
# '-j1' flag to force the build to run sequentially.
RUN stack build

RUN stack install

FROM haskell:8

COPY --from=build /root/.local/bin/duckling-example-exe /root/.local/bin/duckling-example-exe

EXPOSE 8000

CMD duckling-example-exe
