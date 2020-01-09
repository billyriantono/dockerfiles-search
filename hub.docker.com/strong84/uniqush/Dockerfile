FROM centos:7

LABEL maintainer="Double Diamond Team" description="Docker Image for uniqush-push on CentOS"

ENV VERSION 2.6.1

# COPY uniqush-push.conf /etc/uniqush/

RUN curl -sLo uniqush.rpm https://github.com/uniqush/uniqush-push/releases/download/${VERSION}/uniqush-push-${VERSION}-1.x86_64.rpm && \
    rpm -ivh uniqush.rpm && \
    rm -rf /tmp/* /var/tmp/*

EXPOSE 9898

CMD /usr/bin/uniqush-push -config /etc/uniqush/uniqush-push.conf
