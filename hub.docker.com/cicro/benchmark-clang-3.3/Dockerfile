ARG CACHE_TAG=latest

FROM cicro/benchmark-harness:${CACHE_TAG} as harness

FROM cicro/benchmark-base:${CACHE_TAG}

# install our environment for the specific benchmark
RUN apt-add-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty universe" && apt-add-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty main restricted"
RUN apt-get update && apt-get install -y --no-install-recommends clang-3.3 libomp-dev

# our benchmarking project
COPY --from=harness /benchmarks /benchmarks

# configure benchmark environment
RUN echo "CLANG=/usr/bin/clang" >> /benchmarks/configs/env

ENTRYPOINT ["/benchmarks/tools/bench.py", "/data/clang-3.3.json", "--filter-runtime=(clang)", "--suffix=-v3.3"] FOREGROUND
