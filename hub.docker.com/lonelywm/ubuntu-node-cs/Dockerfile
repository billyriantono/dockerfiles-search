FROM ubuntu:18.10

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
	  sudo \
	  zlib1g \
	  zlib1g.dev \
    curl \
	  vim \
	  locales \
	  git \
	  wget \
	  libssl-dev \
	  net-tools \
	  openssh-server \
    ca-certificates \
    libtbb-dev \
    pkg-config \
    libopenexr-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

#-----------------------------------------------------
# Upgrade to gcc 7
# https://gist.github.com/jlblancoc/99521194aba975286c80f93e47966dc5
RUN apt-get update && apt-get install -y software-properties-common gcc g++ \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN     cd /opt && \
        wget https://npm.taobao.org/mirrors/node/v12.9.1/node-v12.9.1-linux-x64.tar.xz && \
        tar -xvf node-v12.9.1-linux-x64.tar.xz && \
        rm node-v12.9.1-linux-x64.tar.xz && \
        mv node-v12.9.1-linux-x64 nodejs && \
        sudo ln -s /opt/nodejs/bin/npm /usr/local/bin && \
        sudo ln -s /opt/nodejs/bin/node /usr/local/bin

ENV PATH="${PATH}:/home/coder/.local/bin"

RUN locale-gen en_US.UTF-8
# We unfortunately cannot use update-locale because docker will not use the env variables
# configured in /etc/default/locale so we need to set it manually.
ENV LC_ALL=en_US.UTF-8

RUN	addgroup --gid 1000 coder; \
 	adduser --uid 1000 --ingroup coder --home /home/coder --shell /bin/bash --disabled-password --gecos "" coder; \
	# Give the coder user sudo access
	usermod -a -G sudo coder; \
	echo "coder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
		
		
# Run as root user, before 'USER coder'
RUN	USER=coder; \
	GROUP=coder; \
	# Get the fixuid package
 	curl -SsL https://github.com/boxboat/fixuid/releases/download/v0.4/fixuid-0.4-linux-amd64.tar.gz | tar -C /usr/local/bin -xzf - && \
	# Make it available globally
	chown root:root /usr/local/bin/fixuid; \
	chmod 4755 /usr/local/bin/fixuid; \
	# Set fixuid configurations
	mkdir -p /etc/fixuid; \
	printf "user: $USER\ngroup: $GROUP\npaths:\n  - /home/coder\n  - /home/coder/workspace" > /etc/fixuid/config.yml

USER coder

RUN     cd /home/coder; \
        # Get the latest version number
        CODER_VERSION=$(basename $(curl -Ls -o /dev/null -w %{url_effective} https://github.com/cdr/code-server/releases/latest)); \
        # Get the latest package based on version number
        wget --quiet https://github.com/cdr/code-server/releases/download/$CODER_VERSION/code-server$CODER_VERSION-linux-x64.tar.gz; \
        # Decompress it
        tar -xvzf code-server$CODER_VERSION-linux-x64.tar.gz; \
        # Make sure it is executable
        chmod +x /home/coder/code-server$CODER_VERSION-linux-x64/code-server; \
        # Make it globally callable
        sudo cp -r /home/coder/code-server$CODER_VERSION-linux-x64/code-server /usr/local/bin; \
        # This solves 'Error: ENOENT: no such file or directory, open '/src/packages/server/build/web/favicon.ico'
        sudo mkdir -p /src/packages/server/build/web; \
        sudo touch /src/packages/server/build/web/favicon.ico; \
        # Cleanup
        rm -rf /home/coder/code-server$CODER_VERSION-linux-x64 /home/coder/code-server$CODER_VERSION-linux-x64.tar.gz

EXPOSE 8443 4200 22 80

WORKDIR /home/coder/workspace

VOLUME [ "/home/coder/workspace" ]

ENTRYPOINT ["fixuid", "code-server", "-e", "/home/coder/.code-server-config"]
