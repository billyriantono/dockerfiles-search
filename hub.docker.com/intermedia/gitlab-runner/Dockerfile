FROM hashicorp/terraform:light AS terraform
FROM gitlab/gitlab-runner:alpine

LABEL maintainer="Alexey Miasoedov <alexey.miasoedov@gmail.com>"

ADD entrypoint-append /
# replace last line <exec gitlab-runner "$@"> with <entrypoint-append> content
RUN sed -i -e '$r /entrypoint-append' -e '$d' /entrypoint
COPY --from=terraform /bin/terraform /bin/

ENV CI_SERVER_URL=""
ENV REGISTRATION_TOKEN=""
ENV RUNNER_TAG_LIST=""