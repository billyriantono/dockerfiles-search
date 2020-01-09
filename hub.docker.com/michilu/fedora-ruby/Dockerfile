FROM michilu/fedora-zero
RUN yum install -y git rubygem-bundler && \
  yum clean all && \
  echo ":ssl_verify_mode: 0" > /etc/gemrc
