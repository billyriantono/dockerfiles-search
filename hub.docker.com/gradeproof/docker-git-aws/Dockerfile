FROM docker:git
LABEL maintainer="Craig Sketchley <craig@gradeproof.com>"

# Install python and the AWS CLI
RUN apk -v --update --no-cache add \
        bash \
        zip \
        curl \
        python \
        py-pip \
        && \
    pip install --upgrade pip && \
    pip install --upgrade awscli
