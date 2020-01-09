FROM fedora:latest

RUN yum update -y \
	&& yum install -y java wget tar rsync @'Development Tools' \
	&& yum -y clean all \
	&& wget https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-5.8.1.tar.gz -O bamboo.tar.gz \
	&& mkdir /opt/bamboo \
	&& tar xf bamboo.tar.gz --strip-components=1 -C /opt/bamboo/ \
	&& rm bamboo.tar.gz \
	&& mkdir -p /var/atlassian/application-data/bamboo \
	&& chown -R 1000:1000 /var/atlassian \
	&& chown -R 1000:1000 /opt/bamboo \
	&& echo 'bamboo.home=/var/atlassian/application-data/bamboo/' >> /opt/bamboo/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties \
	&& chmod -R +x /opt/bamboo/bin/ \
	&& sed -i '1s/^/#!\/bin\/bash\n/' /opt/bamboo/bin/start-bamboo.sh \
	&& useradd bamboo

EXPOSE 8085

VOLUME /var/atlassian

USER bamboo

ENTRYPOINT ["/opt/bamboo/bin/start-bamboo.sh", "-fg"]