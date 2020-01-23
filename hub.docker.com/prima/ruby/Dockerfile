FROM ruby:2.5.1

RUN mkdir -p /aws  && \
	apt-get update && \
	apt-get install -y python-pip python-dev && \
	pip install click boto3 botocore awscli

RUN wget https://github.com/dcoker/biscuit/releases/download/v0.1.3/biscuit-linux_amd64.tgz && \
    tar -xvzf biscuit-linux_amd64.tgz && \
    mv biscuit /usr/local/bin/ && \
    rm -f biscuit-linux_amd64.tgz 

RUN aws configure set default.s3.signature_version s3v4 && \
    aws configure set default.region eu-west-1

COPY files/biscuit_decode.rb /biscuit_decode.rb

RUN chmod 755 /biscuit_decode.rb

ENTRYPOINT ["/bin/bash"]
