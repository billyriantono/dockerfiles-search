FROM node
MAINTAINER xinghen249@gmail.com

RUN cd / && mkdir www conf shell && cd / \
    && curl -o /usr/local/bin/gitlab-runner https://gitlab-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-runner-linux-amd64 \
    && chmod +x /usr/local/bin/gitlab-runner \
    && useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash \
    && gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner \
    && chown -R gitlab-runner /shell

COPY entry.sh /conf/

CMD [ "bash", "/conf/entry.sh" ]
