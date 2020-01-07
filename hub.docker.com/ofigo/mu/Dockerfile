FROM python:slim
RUN apt-get update && \
    apt-get install -y curl && \
    pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    (curl -s https://getmu.io/install.sh | INSTALL_VERSION=1.4.4 INSTALL_DIR=/usr/bin sh) && \
    rm -rf /var/lib/apt/lists/*
VOLUME /root/.aws
CMD ["mu"]
