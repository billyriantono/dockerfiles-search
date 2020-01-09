FROM ubuntu:18.04
LABEL maintainer="matvan@umich.edu"
ENV ACCEPT_EULA=Y
ENV DEBIAN_FRONTEND=noninteractive
# Consider --no-install-recommends on each apt-get install call
RUN apt-get update && \
    apt-get install -qy \
    ca-certificates \
    curl \
    git \
    gnupg2 \
    software-properties-common \
    libpq-dev
RUN apt-add-repository ppa:deadsnakes/ppa -y && \
    apt-get update && \
    apt-get install -qy  \
    python3-pip python3-venv python3-numpy \
    python3.6 python3.6-dev python3.6-venv \
    python3.7 python3.7-dev python3.7-venv python3.7-distutils \
    python3.8 python3.8-dev python3.8-venv python3.8-distutils
# Install MSSQL driver
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > \
    /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get install -qy msodbcsql17 && \
    apt-get install -qy unixodbc-dev
WORKDIR /root
CMD ["sh"]
#     rm -rf /var/cache/apt/lists
