FROM chef/chefdk:current
MAINTAINER Takaaki Furukawa "takaaki.frkw@gmail.com"

RUN apt-get update && apt-get install -y git && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/bin/bash"]
