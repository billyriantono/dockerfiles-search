FROM ubuntu:18.04

RUN apt-get update && apt-get install -y --no-install-recommends \
  htop \
  vim \
  iputils-ping \
  curl \
  dnsutils \
  iperf \
  iproute2 \
  iputils-* \
  nmap \
  net-tools \
  netcat \
  python \
  python-pip \
  python3 \
  python3-pip \
  tcpdump \
  tcpflow \
  traceroute \
  vim \
  wget \
  python-setuptools \
  git \
  zip \
  ssh-client \
  python-all-dev \
  rsync \
  python-wheel \
  && apt-get autoremove -y \
  && rm -rf /var/lib/apt/lists/*

# Health check
RUN pip install flask
ADD health_check.py ./health_check.py
CMD ["python", "health_check.py"]
