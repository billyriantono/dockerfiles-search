FROM alpine
MAINTAINER Michal Belica <devel@beli.sk>
RUN apk --no-cache add bash curl gettext wget \
	&& curl -Lo /usr/local/bin/kubectl \
	https://storage.googleapis.com/kubernetes-release/release/$( \
		curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt \
	)/bin/linux/amd64/kubectl \
	&& chown root:root /usr/local/bin/kubectl && chmod +x /usr/local/bin/kubectl\
	&& HELM_VERSION=$( wget https://github.com/helm/helm/releases/latest --server-response -O /dev/null 2>&1 \
		| awk '/^  Location: /{DEST=$2} END{ print DEST}' | grep -oE "[^/]+$" ) \
	&& echo https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz \
	&& curl -L https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz \
		| tar -C /usr/local/bin --strip-components=1 -zx linux-amd64/helm \
	&& chown root:root /usr/local/bin/helm && chmod +x /usr/local/bin/helm
CMD ["/bin/bash"]
