FROM jenkinsci/jnlp-slave:3.10-1

USER root

# Install package
RUN apt-get update -y && apt-get install -y \
    sudo \
    python-pip \
    ansible \
    make \
 && apt-get -y autoremove && rm -rf /var/lib/apt/lists/*
RUN usermod -aG sudo jenkins \
 && echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
# Install AWS CLI
RUN pip --no-cache-dir install awscli

# Install docker https://docs.docker.com/engine/installation/linux/docker-ce/debian/
RUN apt-get update -y && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
 && apt-get -y autoremove && rm -rf /var/lib/apt/lists/*
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add - \
 && apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable"
RUN apt-get update -y && apt-get install -y \
    docker-ce \
 && apt-get -y autoremove && rm -rf /var/lib/apt/lists/*
RUN usermod -aG docker jenkins

USER jenkins

# Set the following settings to "advanced setting" of Jenkins ECS plugin.
#ENV AWS_DEFAULT_REGION=ap-northeast-1
#ENV http_proxy=
#ENV https_proxy=
#ENV no_proxy=localhost,169.254.169.254,169.254.170.2,/var/run/docker.sock
