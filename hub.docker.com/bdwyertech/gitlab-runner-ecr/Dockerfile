FROM gitlab/gitlab-runner:alpine

RUN wget -nv -q https://github.com/bdwyertech/amazon-ecr-credential-helper/releases/download/bd_update_deps/docker-credential-ecr-login -O /usr/local/bin/docker-credential-ecr-login && chmod +x /usr/local/bin/docker-credential-ecr-login
