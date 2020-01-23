FROM appio/rvm:2.2.0

ENV LANG="C.UTF-8" \
    INSTALL_PATH="/app/public_html" \
    RAILS_ENV="development"

RUN mkdir -p $INSTALL_PATH

WORKDIR $INSTALL_PATH

RUN /bin/bash -lc "rvm --default use 2.2.0"
RUN gem install nokogiri foreman
RUN gem install bundler bundle

RUN echo 127.0.0.1 $VIRTUAL_HOST >> /etc/hosts

RUN mkdir -p config/containers/
COPY config/containers/app_cmd_dev.sh config/containers/
RUN chmod +x config/containers/app_cmd_dev.sh

EXPOSE 3000

CMD ["/bin/bash", "-lc", "$INSTALL_PATH/config/containers/app_cmd_dev.sh"]
