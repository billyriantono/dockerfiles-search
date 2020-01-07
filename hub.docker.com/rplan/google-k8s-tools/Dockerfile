FROM google/cloud-sdk:228.0.0

# kube config volume
VOLUME ["/root/.kube"]

# helm config home
VOLUME ["/root/.helm"]

# install latest helm
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get -o helm_install.sh
RUN chmod +x ./helm_install.sh
RUN ./helm_install.sh --version v2.11.0
