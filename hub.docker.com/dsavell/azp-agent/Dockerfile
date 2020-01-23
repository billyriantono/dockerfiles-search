FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

# Install basic command-line utilities
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    dbus \
    dnsutils \
    dpkg \
    fakeroot \
    file \
    ftp \
    iproute2 \
    iputils-ping \
    jq \
    libcurl4 \
    libgconf-2-4 \
    libsecret-1-dev \
    libunwind8 \
    libxkbfile-dev \
    libxss1 \
    locales \
    netcat \
    openssh-client \
    pkg-config \
    rpm \
    rsync\
    shellcheck \
    software-properties-common \
    sudo \
    telnet \
    time \
    tzdata \
    unzip \
    wget \
    xorriso \
    xvfb \
    xz-utils \
    zip \
    zsync && \
  rm -rf /var/lib/apt/lists/*

# Setup the locale
ENV LANG en_GB.UTF-8
ENV LC_ALL $LANG
RUN locale-gen $LANG \
 && update-locale

# Install build essential tools
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    build-essential && \
  rm -rf /var/lib/apt/lists/*

# Install 7-zip
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    p7zip \
    p7zip-full \
    p7zip-rar && \
  rm -rf /var/lib/apt/lists/*

# Install Ansible PPA and latest Ansible
RUN add-apt-repository -y ppa:ansible/ansible && \
   apt-get update && \
   apt-get install -y --no-install-recommends \
     ansible && \
   rm -rf /var/lib/apt/lists/*

# Install AWS CLI
RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" && \
  unzip awscli-bundle.zip && \
  ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws && \
  rm awscli-bundle.zip && \
  rm -rf awscli-bundle

# Install Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash && \
   rm -rf /var/lib/apt/lists/*

# Install Azure CLI Extentsions
RUN az extension add -n \
  azure-devops

# Install Docker-CE
RUN curl -sSL https://get.docker.com/ | bash && \
  rm -rf /var/lib/apt/lists/*

# Install Docker Compose
RUN DOCKER_COMPOSE_VERSION=$(curl -sX GET "https://api.github.com/repos/docker/compose/releases/latest" | awk '/tag_name/{print $4;exit}' FS='[""]') && \
  curl -L "https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && \
  chmod +x /usr/local/bin/docker-compose

# Install Firefox
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    firefox && \
  rm -rf /var/lib/apt/lists/*

# Install Git
RUN add-apt-repository -y ppa:git-core/ppa && \
   apt-get update && \
   apt-get install -y --no-install-recommends \
     git && \
   rm -rf /var/lib/apt/lists/*

# Install Git LFS
RUN curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
  apt-get install -y --no-install-recommends \
    git-lfs && \
  rm -rf /var/lib/apt/lists/*

# Install Go
RUN curl -sL https://dl.google.com/go/go1.12.14.linux-amd64.tar.gz -o go1.12.14.linux-amd64.tar.gz && \
  mkdir -p /usr/local/go1.12.14 && \
  tar -C /usr/local/go1.12.14 -xzf go1.12.14.linux-amd64.tar.gz --strip-components=1 go && \
  rm go1.12.14.linux-amd64.tar.gz
RUN curl -sL https://dl.google.com/go/go1.13.5.linux-amd64.tar.gz -o go1.13.5.linux-amd64.tar.gz && \
  mkdir -p /usr/local/go1.13.5 && \
  tar -C /usr/local/go1.13.5 -xzf go1.13.5.linux-amd64.tar.gz --strip-components=1 go && \
  rm go1.13.5.linux-amd64.tar.gz
ENV GOROOT_1_12_X64=/usr/local/go1.12.14 \
  GOROOT_1_13_X64=/usr/local/go1.13.5 \
  GOROOT=/usr/local/go1.13.5
ENV PATH $PATH:$GOROOT/bin

# Install Google Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" | tee /etc/apt/sources.list.d/google-chrome.list && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    google-chrome-stable && \
  rm -rf /var/lib/apt/lists/*
ENV CHROME_BIN=/usr/bin/google-chrome

# Install Httpie
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    httpie && \
  rm -rf /var/lib/apt/lists/*

# Install OpenJDK's
ENV DEFAULT_JDK_VERSION=8
RUN apt-add-repository -y ppa:openjdk-r/ppa
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    openjdk-8-jdk && \
  rm -rf /var/lib/apt/lists/*
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    openjdk-11-jdk && \
  rm -rf /var/lib/apt/lists/*
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    openjdk-12-jdk && \
  rm -rf /var/lib/apt/lists/*
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    openjdk-13-jdk && \
  rm -rf /var/lib/apt/lists/*
RUN update-alternatives --set java /usr/lib/jvm/java-${DEFAULT_JDK_VERSION}-openjdk-amd64/jre/bin/java
ENV JAVA_HOME_8_X64=/usr/lib/jvm/java-8-openjdk-amd64 \
  JAVA_HOME_11_X64=/usr/lib/jvm/java-11-openjdk-amd64 \
  JAVA_HOME_12_X64=/usr/lib/jvm/java-12-openjdk-amd64 \
  JAVA_HOME_13_X64=/usr/lib/jvm/java-13-openjdk-amd64 \
  JAVA_HOME=/usr/lib/jvm/java-${DEFAULT_JDK_VERSION}-openjdk-amd64 \
  JAVA_TOOL_OPTIONS=-Dfile.encoding=UTF8

# Install Java Tools
## Install Ant
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    ant \
    ant-optional && \
  rm -rf /var/lib/apt/lists/*

## Install Maven
ENV DEFAULT_MVN_VERSION=3.6.3
RUN curl -sL https://www-eu.apache.org/dist/maven/maven-3/"${DEFAULT_MVN_VERSION}"/binaries/apache-maven-"${DEFAULT_MVN_VERSION}"-bin.zip -o maven.zip && \
  unzip -d /usr/share maven.zip && \
  rm maven.zip && \
  ln -sf /usr/share/apache-maven-"${DEFAULT_MVN_VERSION}"/bin/mvn /usr/bin/mvn
ENV M2_HOME=/usr/share/apache-maven-${DEFAULT_MVN_VERSION}

## Install Gradle
RUN wget -O gradleReleases.html https://gradle.org/releases/ && \
  gradleUrl=$(grep -m 1 -o "https:\/\/services.gradle.org\/distributions\/gradle-.*-bin\.zip" gradleReleases.html | head -1) && \
  gradleVersion=$(echo $gradleUrl | sed -nre 's/^[^0-9]*(([0-9]+\.)*[0-9]+).*/\1/p') && \
  rm gradleReleases.html && \
  curl -sL $gradleUrl -o gradleLatest.zip && \
  unzip -d /usr/share gradleLatest.zip && \
  rm gradleLatest.zip && \
  ln -fs /usr/share/gradle-"${gradleVersion}"/bin/gradle /usr/bin/gradle
ENV GRADLE_HOME=/usr/share/gradle

# Install kubectl
RUN curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
  touch /etc/apt/sources.list.d/kubernetes.list && \
  echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    kubectl && \
  rm -rf /var/lib/apt/lists/*

# Install Helm 3
RUN curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash

# Install MySQL Client
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    mysql-client && \
  rm -rf /var/lib/apt/lists/*

# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash && \
  apt-get install -y --no-install-recommends \
    nodejs -y && \
  rm -rf /var/lib/apt/lists/*

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    yarn && \
  rm -rf /var/lib/apt/lists/*

# Install Packer
RUN PACKER_VERSION=$(curl -s https://checkpoint-api.hashicorp.com/v1/check/packer | jq -r .current_version) && \
  curl -LO "https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip" && \
  unzip -o "packer_${PACKER_VERSION}_linux_amd64.zip" -d /usr/local/bin && \
  rm -f "packer_${PACKER_VERSION}_linux_amd64.zip"

# Install Powershell Core
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb && \
  dpkg -i packages-microsoft-prod.deb && \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    powershell && \
  rm -rf /var/lib/apt/lists/*

# Install Python
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    python \
    python-dev \
    python-pip \
    python3 \
    python3-dev \
    python3-pip && \
  rm -rf /var/lib/apt/lists/*

# Install Subversion
RUN apt-get update && \
  apt-get install -y --no-install-recommends \
    subversion && \
  rm -rf /var/lib/apt/lists/*

# Install Terraform
RUN TERRAFORM_VERSION=$(curl -s https://checkpoint-api.hashicorp.com/v1/check/terraform | jq -r .current_version) && \
  curl -LO "https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip" && \
  unzip -o "terraform_${TERRAFORM_VERSION}_linux_amd64.zip" -d /usr/local/bin && \
  rm -f "terraform_${TERRAFORM_VERSION}_linux_amd64.zip"

# Clean system
RUN apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /etc/apt/sources.list.d/*

# Install Azure Pipelines Agent
COPY root /
WORKDIR /azp
CMD ["./start.sh"]
