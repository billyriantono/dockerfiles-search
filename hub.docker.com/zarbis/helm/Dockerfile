FROM alpine/helm:2.16.1

ENV HELM_HOME /helm
RUN mkdir $HELM_HOME
RUN apk --update add git
RUN helm init --client-only
RUN helm plugin install https://github.com/chartmuseum/helm-push
RUN helm repo remove local
