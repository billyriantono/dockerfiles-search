FROM dogwith1eye/haskell-ide-engine:latest

WORKDIR /root

ADD https://github.com/krallin/tini/releases/download/v0.18.0/tini-static-amd64 /usr/local/sbin/tini

RUN curl -SL -o hlint.tar.gz https://github.com/ndmitchell/hlint/releases/download/v2.2.2/hlint-2.2.2-x86_64-linux.tar.gz \
    && tar -xf hlint.tar.gz \
    && cp hlint-2.2.2/hlint /usr/local/bin/hlint \
    && rm -rf hlint.tar.gz hlint-2.2.2 \
    && chmod u+x /usr/local/sbin/tini \
    && chmod u+x /usr/local/bin/hlint

ENTRYPOINT ["/usr/local/sbin/tini", "--"]
