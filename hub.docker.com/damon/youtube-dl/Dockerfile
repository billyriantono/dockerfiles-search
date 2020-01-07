FROM python:3

RUN apt-get update && \
    apt-get install -y --no-install-recommends libav-tools && \
    rm -Rf /var/lib/apt/lists/* && \
    apt-get clean && \
    apt-get autoremove -y

RUN pip install --upgrade youtube_dl

WORKDIR ["/download"]

ENTRYPOINT ["/usr/local/bin/youtube-dl"]
CMD ["--help"]
