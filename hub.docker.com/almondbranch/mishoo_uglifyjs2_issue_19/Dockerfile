# AWS Elastic Beanstalk Command Line Interface Dockerfile

FROM alpine:3.8

RUN apk --no-cache add \
    # Install awsebcli dependencies:
    py-pip \
    groff \
    less \
    git \
  && pip install --upgrade \
    pip \
    awsebcli \
  # Clean up obsolete files:
  && rm -rf \
    # Clean up any temporary files:
    /tmp/* \
    # Clean up the pip cache:
    /root/.cache \
    # Remove any compiled python files (compile on demand):
    `find / -regex '.*\.py[co]'`

ENTRYPOINT ["eb"]
