FROM circleci/php:7.2-apache-stretch-node-browsers

RUN sudo apt-get update && sudo apt-get install -y awscli groff jq
RUN composer global require "hirak/prestissimo:^0.3"

RUN mkdir -p ~/.terminus/plugins && \
  composer global require pantheon-systems/terminus:^2 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-build-tools-plugin:^2.0.0-beta12 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-secrets-plugin:^1 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-rsync-plugin:^1 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-quicksilver-plugin:^1 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-composer-plugin:^1 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-drupal-console-plugin:^1 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-mass-update:^1 && \
  composer -n create-project -d ~/.terminus/plugins pantheon-systems/terminus-site-clone-plugin:^2

ENV TERMINUS_PLUGINS_DIR="~/.terminus/plugins"
ENV PATH="~/.composer/vendor/bin:${PATH}"
