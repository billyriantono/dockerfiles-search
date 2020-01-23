FROM 6zar/pyspark
# Source: https://docs.docker.com/install/linux/docker-ce/ubuntu/
RUN apt-get update
RUN apt-get update && apt-get install -y  apt-transport-https \
    ca-certificates curl gnupg-agent software-properties-common ssh \
    && rm -rf /var/lib/apt/lists/*
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
RUN apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io \
    && rm -rf /var/lib/apt/lists/*
# This may not work on ARM servers
RUN pip install pandas
# Source: https://docs.docker.com/compose/install/
RUN curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
RUN ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
CMD cd /root && jupyter notebook  --ip=0.0.0.0 --allow-root
