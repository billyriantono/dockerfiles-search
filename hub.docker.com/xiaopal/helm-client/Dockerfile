# v2.9.1
FROM alpine:3.7

RUN apk add --no-cache bash coreutils curl openssh-client openssl git findutils && \
	curl -sSL 'http://npc.nos-eastchina1.126.net/dl/jq_1.5_linux_amd64.tar.gz' | tar -zx -C /usr/local/bin && \
	curl -sSL 'https://npc.nos-eastchina1.126.net/dl/kubernetes-client-v1.9.3-linux-amd64.tar.gz' | tar -zx -C /usr/local && \
	mkdir -p /usr/local/helm && \
	curl -sSL 'https://npc.nos-eastchina1.126.net/dl/helm-v2.9.1-linux-amd64.tar.gz' | tar -zx -C /usr/local/helm
ENV KUBECTL_EXECUTABLE=/usr/local/kubernetes/client/bin/kubectl HELM_EXECUTABLE=/usr/local/helm/linux-amd64/helm

ADD exec-cmd.sh /usr/local/
RUN chmod 0755 /usr/local/exec-cmd.sh && \
	ln -s /usr/local/exec-cmd.sh /usr/local/bin/helm && \
	ln -s /usr/local/exec-cmd.sh /usr/local/bin/kubectl
CMD [ "/bin/bash" ]