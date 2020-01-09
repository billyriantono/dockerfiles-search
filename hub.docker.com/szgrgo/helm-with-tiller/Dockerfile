FROM alpine

ENV HELM_VERSION="v2.11.0"
ENV BASE_DIR="/helm-runner"
ENV TAR="helm-${HELM_VERSION}-linux-amd64.tar.gz"
ENV WGET_URL="https://storage.googleapis.com/kubernetes-helm/${TAR}"

ENV HELM_HOME="${BASE_DIR}/.helm"
ENV KUBECONFIG="${BASE_DIR}/.kube/config"
ENV HELM_HOST="localhost:44134"

RUN mkdir -p ${BASE_DIR}
RUN mkdir -p ${HELM_HOME}/plugins
RUN mkdir -p ${BASE_DIR}/.kube

WORKDIR ${BASE_DIR}
RUN apk add --update ca-certificates \
	&& apk add wget bash gettext git \
	&& wget ${WGET_URL} \
	&& tar -xvf ${TAR} \
	&& mv  linux-amd64/helm linux-amd64/tiller /usr/local/bin \
	&& rm /var/cache/apk/* \
	&& rm -f ${TAR} \
	&& rm -rf linux-amd64 \
	&& apk del wget

COPY config.tpl init.sh ${BASE_DIR}/
RUN chmod +x init.sh
RUN helm plugin install https://github.com/rimusz/helm-tiller
RUN helm plugin install https://github.com/chartmuseum/helm-push

CMD ${BASE_DIR}/init.sh && tail -f /dev/null
