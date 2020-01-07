FROM alpine:3.6

RUN apk --update add monit nmap nmap-scripts curl tcpdump bind-tools jq nmap-ncat libcap && \
rm -rf /var/cache/apk/*

#Get kubectl modify the version for later ones, and damn but this is a big binary!
RUN curl -O https://storage.googleapis.com/kubernetes-release/release/v1.8.0/bin/linux/amd64/kubectl && \
chmod +x kubectl && mv kubectl /usr/local/bin

#Get docker we're not using the apk as it includes the server binaries that we don't need
RUN curl -O https://download.docker.com/linux/static/stable/x86_64/docker-17.12.1-ce.tgz && tar -xzvf docker-17.12.1-ce.tgz && \
cp docker/docker /usr/local/bin && chmod +x /usr/local/bin/docker && rm -rf docker/ && rm -f docker-17.12.1-ce.tgz

#Get etcdctl
RUN curl -OL https://github.com/coreos/etcd/releases/download/v3.1.5/etcd-v3.1.5-linux-amd64.tar.gz && \
tar -xzvf etcd-v3.1.5-linux-amd64.tar.gz && cp etcd-v3.1.5-linux-amd64/etcdctl /usr/local/bin && \
chmod +x /usr/local/bin/etcdctl && rm -rf etcd-v3.1.5-linux-amd64 && rm -f etcd-v3.1.5-linux-amd64.tar.gz

#Get oc
RUN curl -OL https://github.com/openshift/origin/releases/download/v3.7.1/openshift-origin-client-tools-v3.7.1-ab0f056-linux-64bit.tar.gz && \
tar -xzvf openshift-origin-client-tools-v3.7.1-ab0f056-linux-64bit.tar.gz && cp openshift-origin-client-tools-v3.7.1-ab0f056-linux-64bit/oc /usr/local/bin && \
chmod +x /usr/local/bin/oc && rm -rf oopenshift-origin-client-tools-v3.7.1-ab0f056-linux-64bit && rm -f openshift-origin-client-tools-v3.7.1-ab0f056-linux-64bit.tar.gz

#Get AmIcontained
RUN curl -OL https://github.com/jessfraz/amicontained/releases/download/v0.0.8/amicontained-linux-amd64 && \
cp amicontained-linux-amd64 /usr/local/bin/amicontained && chmod +x /usr/local/bin/amicontained


#create our new user
RUN adduser -S tester

#set the workdir, why not
WORKDIR /home/tester

USER tester

# This is a Dumb Hack
CMD ["tail", "-f" , "/dev/null"]
