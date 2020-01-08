FROM amazonlinux:2
LABEL maintainer="rajesh.jonnalagadda@phenompeople.com" \
      version="10.15.0"
ARG APP_HOME=/opt/deployment
RUN yum install -q -y  wget shadow-utils tar gzip xz fontconfig && \
	mkdir -p /opt/phenom/scripts && \
  	groupadd phenom -g 505 && \ 
	useradd -u 504 -g 505 -d ${APP_HOME} phenom
ARG NODE_VERSION=v10.15.0
ENV NODE_VERSION=${NODE_VERSION}
RUN wget -q -O /tmp/node.tar.xz http://nodejs.org/dist/${NODE_VERSION}/node-${NODE_VERSION}-linux-x64.tar.xz && \
	tar -xJf /tmp/node.tar.xz -C /usr/local && \
	ln -sf /usr/local/node-${NODE_VERSION}-linux-x64 /usr/local/node && \
	rm -rf /tmp/node.tar.xz
ENV PATH=/usr/local/node/bin:$PATH
ENTRYPOINT ["node"]
