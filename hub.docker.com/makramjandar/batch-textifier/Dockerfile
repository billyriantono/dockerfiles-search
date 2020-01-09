FROM makramjandar/glibc

RUN apk add --no-cache bash ca-certificates gcc python wget xdg-utils xz \
    && wget -nv -O- https://download.calibre-ebook.com/linux-installer.py | python -c "import sys; main=lambda:sys.stderr.write('Download failed\n'); exec(sys.stdin.read()); main()" \
    && mkdir -p /corpora && wget -nv -O /batchTextifier.py https://git.io/JeRGD \
    && rm -rf  /tmp/calibre-installer-cache /root/.wget-hsts

ENV PATH /:$PATH

WORKDIR /
VOLUME ["/corpora"]
ENTRYPOINT ["ebook-convert"]
CMD ["python", "batchTextifier.py"]
