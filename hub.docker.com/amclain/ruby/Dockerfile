FROM amclain/rbenv
MAINTAINER Alex McLain <alex@alexmclain.com>

ONBUILD ADD docker/install_ruby_version /root/install_ruby_version
ONBUILD RUN cd $RBENV_PATH; git pull
ONBUILD RUN cd ${RBENV_PATH}/plugins/ruby-build; git pull
ONBUILD RUN rbenv install "$(cat /root/install_ruby_version)" -v
ONBUILD RUN rbenv global "$(cat /root/install_ruby_version)"
ONBUILD RUN echo "gem: --no-rdoc" > ~/.gemrc
ONBUILD RUN gem update --force
ONBUILD RUN gem update --system --force
