FROM docker:stable

RUN apk --no-cache add git py-pip python-dev libffi-dev openssl-dev gcc libc-dev make bash curl
RUN pip install docker-compose

# Install Helm
USER root
RUN cd /home \
	&& curl https://storage.googleapis.com/kubernetes-helm/helm-v2.2.3-linux-amd64.tar.gz -o helm.tar.gz \
	&& tar -xvf helm.tar.gz \
	&& rm helm.tar.gz \
	&& mv linux-amd64/helm /usr/local/bin/helm \
	&& chmod +x /usr/local/bin/helm

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]
