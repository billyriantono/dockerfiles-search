FROM alpine:3.6
MAINTAINER devops@leonisand.co

ENV TF_VER 0.10.7
ENV BIN_DIR /root/.local/bin
ENV TF_PLUGIN_CACHE_DIR=/root/.terraform.d/plugin-cache

RUN apk add --no-cache curl make git ca-certificates jq bash && \
  mkdir -p ${BIN_DIR} && \
  mkdir -p ${TF_PLUGIN_CACHE_DIR} && \
  curl -L https://releases.hashicorp.com/terraform/${TF_VER}/terraform_${TF_VER}_linux_amd64.zip > ${BIN_DIR}/terraform_${TF_VER}.zip && \
  unzip ${BIN_DIR}/terraform_${TF_VER}.zip -d ${BIN_DIR} && rm ${BIN_DIR}/*.zip

ENTRYPOINT ["/root/.local/bin/terraform"]

CMD ["help"]
