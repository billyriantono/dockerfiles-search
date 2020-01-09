FROM maven:3-jdk-8-slim

ADD 'https://api.bintray.com/content/jfrog/jfrog-cli-go/$latest/jfrog-cli-linux-amd64/jfrog?bt_package=jfrog-cli-linux-amd64' /usr/local/bin/jfrog
ADD semver /usr/local/bin/semver
ADD kiya /usr/local/bin/kiya
RUN chmod 755 /usr/local/bin/jfrog /usr/local/bin/semver /usr/local/bin/kiya

RUN apt-get update && apt-get install -y \
	git \
	lsb-release \
	gnupg2

RUN echo "deb http://packages.cloud.google.com/apt cloud-sdk-$(lsb_release -c -s) main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
RUN apt-get update && apt-get install -y \
	google-cloud-sdk \
	kubectl \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /root/.jfrog /root/.config/gcloud
