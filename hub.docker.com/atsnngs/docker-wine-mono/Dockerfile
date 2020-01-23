FROM electronuserland/builder:wine-mono

RUN apt-get update -y && \
    apt-get install osslsigncode xvfb -y --no-install-recommends && \
    apt-get clean && rm -rf /var/lib/apt/lists/*
