FROM microsoft/azure-cli
RUN apk add --no-cache bash-completion \
 && echo -e "\nsource /usr/share/bash-completion/bash_completion" >> ~/.bashrc
RUN which kubectl || az aks install-cli
RUN test -f /usr/share/bash-completion/completions/kubectl || kubectl completion bash > /usr/share/bash-completion/completions/kubectl
RUN which helm || curl https://raw.githubusercontent.com/helm/helm/master/scripts/get | bash
RUN test -f /usr/share/bash-completion/completions/helm || helm completion bash > /usr/share/bash-completion/completions/helm


