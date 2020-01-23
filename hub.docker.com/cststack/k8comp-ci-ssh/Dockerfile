FROM jenkins/ssh-slave
ENV KUBE_VERSION v1.8.4
ENV OC_VERSION v3.6.1
ENV OC_TAG 008f2d5
ENV YQ_VERSION 1.14.0
ENV K8COMP_VERSION master
ENV HELM_VERSION 2.7.2
RUN apt-get update && \
    apt-get install rubygems ed jq -y && \
    gem install hiera hiera-eyaml && \
    curl -L  https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VERSION}-linux-amd64.tar.gz| tar -xz && \
    mv linux-amd64/helm /bin/ && \
    curl -L -o /bin/kubectl https://storage.googleapis.com/kubernetes-release/release/${KUBE_VERSION}/bin/linux/amd64/kubectl && \
    curl -L -o /bin/yq  https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64 && \
    curl -L  https://github.com/openshift/origin/releases/download/${OC_VERSION}/openshift-origin-client-tools-${OC_VERSION}-${OC_TAG}-linux-64bit.tar.gz | tar -xz && \
    mv openshift-origin-client-tools-${OC_VERSION}-${OC_TAG}-linux-64bit/oc /bin/oc && \
    curl -L -o /bin/k8comp https://raw.githubusercontent.com/cststack/k8comp/${K8COMP_VERSION}/bin/k8comp && \
    chmod +x /bin/* && \
    rm -rf /var/cache/* && \
    echo "jenkins:jenkins" | chpasswd && \
    echo "root:jenkins" | chpasswd && \
    sed -i 's/PermitRootLogin.*/#PermitRootLogin/' /etc/ssh/sshd_config && \
    sed -i 's/PasswordAuthentication.*/#PasswordAuthentication/' /etc/ssh/sshd_config
