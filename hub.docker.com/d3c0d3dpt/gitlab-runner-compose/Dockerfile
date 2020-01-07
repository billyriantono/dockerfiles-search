FROM tmaier/docker-compose

ADD https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-ci-multi-runner-linux-amd64 /usr/local/bin/gitlab-ci-multi-runner
RUN chmod +x /usr/local/bin/gitlab-ci-multi-runner
RUN ln -s /usr/local/bin/gitlab-ci-multi-runner /usr/local/bin/gitlab-runner

CMD ["gitlab-runner", "run"]
