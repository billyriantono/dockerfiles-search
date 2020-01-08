FROM maven:3.6.1-jdk-11

LABEL manitainer="Apontador Team"


RUN curl -fsSL https://get.docker.com -o get-docker.sh \
    && sh get-docker.sh \
    && rm get-docker.sh \
    && useradd -M -N -u 1000 apontador \
    && usermod -aG docker apontador \
    && rm -rf /var/lib/apt/lists/*
