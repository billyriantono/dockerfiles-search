FROM bitnami/redmine:latest

LABEL maintainer "Kehao Chen <kehao.chen@happyhacking.ninja>"

ARG CODE_REVIEW_URL=https://github.com/haru/redmine_code_review/releases/download/0.9.0/redmine_code_review-0.9.0.zip
ARG MESSENGER_URL=https://github.com/AlphaNodes/redmine_messenger/archive/1.0.2.zip

WORKDIR /opt/bitnami/redmine

COPY plugins/redmine_agile-1_4_6-light.zip redmine_agile.zip
COPY plugins/redmine_checklists-3_1_11-light.zip redmine_checklists.zip

RUN \
  apt-get update && \
  apt-get install -y curl unzip && \
  curl -SL ${CODE_REVIEW_URL} -o redmine_code_review.zip && \
  curl -SL ${MESSENGER_URL} -o redmine_messenger.zip && \
  unzip -d /opt/bitnami/redmine/plugins redmine_agile.zip && \
  unzip -d /opt/bitnami/redmine/plugins redmine_checklists.zip && \
  unzip -d /opt/bitnami/redmine/plugins redmine_code_review.zip && \
  unzip -d /opt/bitnami/redmine/plugins redmine_messenger.zip && \
  mv /opt/bitnami/redmine/plugins/redmine_messenger-1.0.2 /opt/bitnami/redmine/plugins/redmine_messenger && \
  rm redmine_agile.zip redmine_checklists.zip redmine_code_review.zip redmine_messenger.zip
RUN \
  apt-get install -y default-libmysqlclient-dev libpq-dev pkg-config libmagickwand-dev && \
  install_packages build-essential default-libmysqlclient-dev libpq-dev pkg-config libmagickwand-dev && \
  bundle install --without development test --no-deployment && \
  rm -rf /var/lib/apt/lists/*