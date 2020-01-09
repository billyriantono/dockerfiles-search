FROM google/cloud-sdk

# Install yamllint
COPY requirements.txt /
RUN pip install -r requirements.txt

# Install kubeval
RUN curl -LO https://github.com/instrumenta/kubeval/releases/download/0.13.0/kubeval-linux-amd64.tar.gz
RUN tar xf kubeval-linux-amd64.tar.gz
RUN mv kubeval /usr/local/bin

# Install colordiff
RUN apt-get install colordiff
