FROM patatra/nodejs

RUN apt-get update && apt-get install -y \
		imagemagick \
		rbenv \
	&& rm -rf /var/lib/apt/lists/*

RUN npm install -g bower@1.4.1 \
    pm2@0.15.7 \
    node-inspector@0.12.2 \
    grunt-cli

RUN gem install sass --version 3.2.10

# Create a nonroot user, and switch to it
RUN /usr/sbin/useradd --create-home --home-dir /usr/local/nonroot --shell /bin/bash nonroot

# Switch to our nonroot user
USER nonroot

WORKDIR /var/app

EXPOSE 3000
