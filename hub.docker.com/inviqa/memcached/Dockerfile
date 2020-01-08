FROM inviqa/base
MAINTAINER Mike Simons <msimons@inviqa.com>

RUN yum install -y memcached && yum clean all

EXPOSE 11211

CMD ["memcached", "-u", "memcached"]
