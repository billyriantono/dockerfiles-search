#
# Atlassian Data Center products Dockerfile
#
FROM store/oracle/serverjre:8

# Every data center application needs:
#  - Database drivers: Postgres, SQL Server, Oracle (MySQL is not supported by Atlassian Data Center)
#  - Shared volume: for AWS, that's EFS. for GCP, that's Gluster: containers
#  - Load balancer: for AWS, that's ALB. for GCP, that's 

# gcloud docker -- pull gcr.io/google-containers/volume-gluster:latest

# https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/
# https://github.com/FuriKuri/docker-best-practices

# Valid options: jira (confluence synchrony bitbucket)
ENV PRODUCT jira
ENV VERSION 7.6.2
ENV DEBUG true

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r $PRODUCT && useradd -r -g $PRODUCT $PRODUCT \
    && mkdir -p /opt/atlassian \
    && mkdir -p /var/atlassian/application-data/$PRODUCT \
    && chown -R $PRODUCT.$PRODUCT /opt/atlassian /var/atlassian \
    && yum install -y\
	vim\
	augeas\
	tar\
	gzip\
#    && yum clean all\
     && cp /usr/share/augeas/lenses/dist/xml.aug /usr/share/augeas/lenses/dist/xml.aug.original\
     && awk "/let filter =/{print;print \". (incl \\\"/opt/atlassian/$PRODUCT/conf/*.xml\\\")\";next}1" /usr/share/augeas/lenses/dist/xml.aug.original >/usr/share/augeas/lenses/dist/xml.aug\
     && rm /usr/share/augeas/lenses/dist/xml.aug.original

USER $PRODUCT

ADD cli /opt/atlassian/cli
ADD docker-entrypoint.sh /opt/atlassian/

ENTRYPOINT ["/opt/atlassian/docker-entrypoint.sh"]

#CMD ["/bin/bash"]

