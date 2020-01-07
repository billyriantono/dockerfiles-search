FROM centos:7
MAINTAINER John Pape <jpapejr@icloud.com>

ADD entrypoint.sh /usr/share/eclipse/entrypoint.sh
ADD stack.sh	/usr/share/eclipse/stack.sh

RUN yum -y install java unzip && yum -y clean all
RUN curl -L "http://ftp.osuosl.org/pub/eclipse/orion/drops/R-12.0-201606220105/eclipse-orion-12.0-linux.gtk.x86_64.zip" \
    -o /tmp/eclipse-orion-12.0-linux.gtk.x86_64.zip \
    && cd /usr/share \
    && unzip /tmp/eclipse-orion-12.0-linux.gtk.x86_64.zip

RUN yum install -y wget socat docker \
		&& wget https://raw.githubusercontent.com/eclipse/orion.client/master/bundles/org.eclipse.orion.client.core/web-ide.conf \
		&& mv web-ide.conf /usr/share/eclipse/orion.conf \
		&& echo "-Dorion.core.configFile=/usr/share/eclipse/orion.conf" >> /usr/share/eclipse/orion.ini \
		&& sed -i 's/serverworkspace/\/workspace/' /usr/share/eclipse/orion.ini \
		&& sed -i 's/#orion.auth.admin.default.password={password}/orion.auth.admin.default.password=passw0rd/' /usr/share/eclipse/orion.conf \
		&& sed -i 's/#orion.auth.log.service=admin/orion.auth.log.service=admin/' /usr/share/eclipse/orion.conf \
		&& sed -i 's/#orion.file.defaultSCM=git/orion.file.defaultSCM=git/'  /usr/share/eclipse/orion.conf \
		&& sed -i 's/#orion.file.diskUsageEnabled=true/orion.file.diskUsageEnabled=true/' /usr/share/eclipse/orion.conf \
		# && echo "orion.core.docker.uri=tcp://localhost:2375" >> /usr/share/eclipse/orion.conf \
		&& chmod +x /usr/share/eclipse/entrypoint.sh \
		&& chmod +x /usr/share/eclipse/stack.sh \
		&& ln -s /usr/share/eclipse/stack.sh /usr/local/bin/stack

WORKDIR /usr/share/eclipse

VOLUME /workspace

CMD ["./entrypoint.sh"]
EXPOSE 8080

