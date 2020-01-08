FROM alpine

ARG VERSION
ARG COMMIT
ARG URL
ARG BRANCH
ARG DATE

LABEL       org.label-schema.name="etcdctl"                                                         \
            org.label-schema.description="etcdctl - swiss army knife (cli) for etcd clusters" \
            org.label-schema.build-date=$DATE                                                       \
            org.label-schema.vcs-ref=$COMMIT                                                        \
            org.label-schema.vcs-url=$URL                                                           \
            org.label-schema.vendor="@lwieske"

RUN \
            addgroup -g 1000 -S user                                                                     && \
            adduser -S -G user -u 1000 -s /bin/sh -h /home/user user                                     && \
            mkdir -p /home/user/bin /home/user/.kube                                                     && \
            apk add --no-cache --virtual=build-dependencies ca-certificates curl                         && \
            curl -L https://github.com/etcd-io/etcd/releases/download/$VERSION/etcd-$VERSION-linux-amd64.tar.gz | \
            tar xz etcd-$VERSION-linux-amd64/etcdctl --strip-components=1 -C /home/user/bin              && \
            mkdir -p /etc/kubernetes/pki/etcd                                                            && \
            chown root:root /etc/kubernetes/pki/etcd                                                     && \
            apk del build-dependencies                                                                   && \
            chmod u+x /home/user/bin/etcdctl                                                             && \
            chown -R user:user /home/user

USER        user
ENV         HOME    /home/user
ENV         USER    user
ENV         PATH    "/home/user/bin:${PATH}"

WORKDIR     /home/user
VOLUME      /home/user/.kube

ENTRYPOINT  ["/home/user/bin/etcdctl"]