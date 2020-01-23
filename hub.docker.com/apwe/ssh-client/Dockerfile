FROM ubuntu:latest
RUN ["apt-get", "update", "-y"]
RUN ["apt-get", "install", "openssh-client", "curl", "wget", "gnupg", "apt-transport-https", "apt-utils", "less", "zip", "unzip", "nano", "dnsutils", "-y"]
RUN ["wget", "https://packages.cloud.google.com/apt/doc/apt-key.gpg"]
RUN ["apt-key", "add", "apt-key.gpg"]
RUN sh -c 'echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | tee -a /etc/apt/sources.list.d/kubernetes.list'
RUN ["cat", "/etc/apt/sources.list.d/kubernetes.list"]
RUN ["apt-get", "update", "-y"]
RUN ["apt-get", "install", "kubectl", "-y"]
