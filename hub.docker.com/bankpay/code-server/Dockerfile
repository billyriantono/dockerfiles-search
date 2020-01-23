# We deploy with ubuntu so that devs have a familiar environment.
FROM ubuntu:18.04

# Install VS Code's deps. These are the only two it seems we need.
RUN apt-get update && apt-get install -y \
	libxkbfile-dev \
	libsecret-1-dev \
	openssl \
	net-tools \
	git \
	locales \
	sudo \
	dumb-init \
	vim \
	curl \
	wget \
	python3 \
	groff

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "LANG=en_US.UTF-8" >> /etc/environment
RUN echo "NODE_ENV=development" >> /etc/environment
RUN more "/etc/environment"
#RUN locale-gen en_US en_US.UTF-8
#RUN dpkg-reconfigure locales


RUN locale-gen en_US.UTF-8
# We unfortunately cannot use update-locale because docker will not use the env variables
# configured in /etc/default/locale so we need to set it manually.
ENV LC_ALL=en_US.UTF-8



# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install --yes nodejs zsh gcc g++ make
RUN node -v && npm -v

# Ensure latest yarn.
RUN npm install -g yarn @aws-amplify/cli serverless --unsafe-perm=true


WORKDIR /code-server
RUN wget https://github.com/cdr/code-server/releases/download/2.1650-vsc1.39.2/code-server2.1650-vsc1.39.2-linux-x86_64.tar.gz
RUN tar -xvf code-server2.1650-vsc1.39.2-linux-x86_64.tar.gz
RUN cp /code-server/code-server2.1650-vsc1.39.2-linux-x86_64/code-server /usr/local/bin/code-server

RUN addgroup --group bankpay \
    && adduser --ingroup bankpay --shell /bin/zsh --disabled-password bankpay \
	&& echo "bankpay ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/nopasswd

USER bankpay
# We create first instead of just using WORKDIR as when WORKDIR creates, the user is root.
WORKDIR /home/bankpay
RUN sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
COPY .zshrc /home/bankpay/.zshrc
ENV PATH="/home/bankpay/.local/bin:${PATH}"
RUN curl -O https://bootstrap.pypa.io/get-pip.py \
	&& python3 get-pip.py --user \
	&& pip install awscli --upgrade --user \
	&& aws --version

RUN mkdir -p /home/bankpay/workspace

WORKDIR /home/bankpay/workspace
EXPOSE 8443

ENTRYPOINT ["dumb-init", "code-server"]