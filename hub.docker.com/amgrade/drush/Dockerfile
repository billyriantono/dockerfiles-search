FROM amgrade/phpcli

ENV HOME /root

# install drush, CodeSniffer, code
RUN composer global require drush/drush:dev-master
RUN composer global require squizlabs/PHP_CodeSniffer:\<2
RUN composer global require drupal/coder:\<8

# add composer bin folder to $PATH
ENV PATH $HOME/.composer/vendor/bin:$PATH

# configure drupal standards
RUN phpcs --config-set installed_paths $HOME/.composer/vendor/drupal/coder/coder_sniffer
