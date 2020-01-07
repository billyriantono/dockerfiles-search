FROM google/cloud-sdk:alpine

RUN gcloud components install kubectl

RUN curl -s https://api.github.com/repos/kubernetes-sigs/kustomize/releases/latest |\
  grep browser_download_url |\
  grep linux |\
  cut -d '"' -f 4 |\
  xargs wget -O - -q > /usr/local/bin/kustomize

RUN chmod u+x /usr/local/bin/kustomize