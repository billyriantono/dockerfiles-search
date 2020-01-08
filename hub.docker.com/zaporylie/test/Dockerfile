FROM drupaldocker/drush:8
MAINTAINER drupal-docker <info@drupaldocker.org>

COPY behat.sh /root/tests/

RUN composer global require drupal/drupal-extension:~3.0 \
 && chmod +x /root/tests/behat.sh

ENV TEST_DIR=/var/www/html/tests \
 BASE_URL="http://app" \
 DRUPAL_ROOT=/var/www/html

CMD ["/root/tests/behat.sh"]
