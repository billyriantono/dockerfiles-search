FROM arcaneio/kubectl:azure-cli

RUN apk upgrade && \
    curl -L https://storage.googleapis.com/kubernetes-helm/helm-$(curl -s "https://api.github.com/repos/helm/helm/releases" | jq -rc '[.[] | select( .prerelease == false ) .tag_name] | .[0]')-linux-amd64.tar.gz > helm.tar.gz \
    && tar xzvf helm.tar.gz && cd linux-amd64 \
    && chmod +x ./* \
    && mv ./helm /usr/local/bin/helm \
    && mv ./tiller /usr/local/bin/tiller \
    && cd .. && rm -rf linux-amd64 && rm -f helm.tar.gz