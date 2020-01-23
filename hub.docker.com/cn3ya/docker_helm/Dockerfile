FROM google/cloud-sdk:alpine
WORKDIR /app
RUN gcloud components install kubectl \
&& apk add --no-cache openssl \
&& curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get > install_helm.sh
CMD ["sh"]