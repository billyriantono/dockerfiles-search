FROM mgit/base:ansible-stable
LABEL maintainer="Alexander Skiba <alexander.skiba@timetac.com>"

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
  && apt-get install --yes --quiet --no-install-recommends \
    "python3" \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
