FROM alpine:latest

RUN \
	apk -Uuv add groff less python py2-pip bash jq mysql-client curl wget && \
	pip install awscli yq==2.1.1 && \
	apk --purge -v del py2-pip && \
	rm /var/cache/apk/*

# Install pip and yq
# RUN wget https://bootstrap.pypa.io/get-pip.py; python get-pip.py
# RUN pip install 'yq'

# Install Kubernetes kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

# Install Kubernetes kops
RUN wget -O /usr/bin/kops https://github.com/kubernetes/kops/releases/download/1.5.3/kops-linux-amd64; chmod +x /usr/bin/kops
