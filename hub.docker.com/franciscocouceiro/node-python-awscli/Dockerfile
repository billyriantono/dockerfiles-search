FROM beevelop/nodejs:v8.11.4

# Install Python.
RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*

# Install aws cli
RUN pip install awscli
