FROM ubuntu:bionic

ARG GH_RUNNER_VERSION="2.160.2"

# Install prerequisites
RUN apt-get update && apt-get install -y curl sudo

# Create github user and pull runner binary
RUN useradd github \
	&& echo "github ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers \
	&& usermod -aG sudo github \
	&& mkdir /app \
	&& cd /app \
	&& curl -O https://githubassets.azureedge.net/runners/${GH_RUNNER_VERSION}/actions-runner-linux-x64-${GH_RUNNER_VERSION}.tar.gz \
	&& tar xzf ./actions-runner-linux-x64-*.tar.gz \
	&& bash /app/bin/installdependencies.sh \
	&& chown -R github:github /app

WORKDIR /app

# Prepare entrypoint
COPY entrypoint.sh /app/entrypoint.sh
RUN chown github:github /app/entrypoint.sh \
	&& chmod +x /app/entrypoint.sh

USER github
ENTRYPOINT ["/app/entrypoint.sh"]
