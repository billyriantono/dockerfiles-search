FROM python:3

LABEL maintainer="guillaume@van-hemmen.com"

RUN echo "installing AWS CLI..." && \
    apt-get update && \
    apt-get install -y groff && \ 
    pip3 install awscli && \
    echo "=========\nAWS VERSION:" && \
    aws --version && \
    echo "Done"

ENTRYPOINT ["aws"]
