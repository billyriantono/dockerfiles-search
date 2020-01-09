FROM dtzar/helm-kubectl:2.13.0

ENV HELM_HOME /home/helm/
RUN mkdir -p /home/helm/plugins
RUN helm plugin install https://github.com/chartmuseum/helm-push
