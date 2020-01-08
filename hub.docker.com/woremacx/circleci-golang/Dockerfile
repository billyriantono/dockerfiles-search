FROM circleci/golang:1.11.2
# MAINTAINER ops@spaceback.me

# Install awscli
# http://docs.aws.amazon.com/cli/latest/userguide/awscli-install-bundle.html
RUN wget "s3.amazonaws.com/aws-cli/awscli-bundle.zip" -O "awscli-bundle.zip" && \
    unzip awscli-bundle.zip && \
    # Workaround to get awscli to work properly
    # https://github.com/aws/aws-cli/issues/1957#issuecomment-271057166
    sudo apt-get install groff-base && \
    sudo ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws && \
    rm awscli-bundle.zip && \
    rm -rf awscli-bundle

ENTRYPOINT ["/bin/bash"]
