FROM amazonlinux:2

# Install prerequisites
RUN yum install -y curl sudo tar gzip shadow-utils \
    && yum install -y lttng-ust openssl-libs krb5-libs zlib libicu \
    && yum clean all && rm -rf /var/cache/yum

# Create github user and pull runner binary
RUN useradd github \
	&& echo "github ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers \
	&& usermod -aG wheel github \
	&& mkdir /app \
	&& cd /app \
	&& curl -O https://githubassets.azureedge.net/runners/2.161.0/actions-runner-linux-x64-2.161.0.tar.gz \
	&& tar xzf ./actions-runner-linux-x64-*.tar.gz \
	&& rm ./actions-runner-linux-x64-*.tar.gz \
	&& chown -R github:github /app

# Prepare entrypoint
COPY entrypoint.sh /app/entrypoint.sh
RUN chown github:github /app/entrypoint.sh \
	&& chmod +x /app/entrypoint.sh
USER github
ENTRYPOINT ["/app/entrypoint.sh"]
