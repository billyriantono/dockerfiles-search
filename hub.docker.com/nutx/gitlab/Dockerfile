FROM sameersbn/gitlab:12.3.5

COPY ./zh.diff .

RUN apt-get update \
    && apt-get install --no-install-recommends -y patch \
    && patch -d . -p1 < zh.diff \
    && rm -rf zh.diff \
    && rm -rf /var/lib/apt/lists/*

