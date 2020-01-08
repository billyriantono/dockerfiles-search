FROM deepwoods/centos7

LABEL Maintainer="Rob Asher - DeepWoods"

RUN yum -y install nxcloud && \
    yum clean all && \
    rm -rf /var/cache/yum

ENTRYPOINT ["/bin/bash"]
CMD ["/nxcloud/bin/startup.sh"]