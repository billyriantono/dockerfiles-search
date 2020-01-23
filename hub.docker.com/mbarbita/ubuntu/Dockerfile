FROM ubuntu
ENV LANG C.UTF-8
RUN apt-get update \
    && apt-get install -y mc nano openssh-client apt-utils \
    && apt-get autoclean \
    && rm -rf /var/lib/apt/lists/*
CMD ["/bin/bash"]
