FROM walm/base:0.1.1
MAINTAINER Andreas Wålm "andreas@walm.net"

RUN bash -c ' \
  apt-get update -qq ;\
  \
  echo "# Installing RVM" ;\
  ln -sf /proc/self/fd /dev/fd ;\
  curl -sSL https://get.rvm.io | bash -s stable ;\
  source /etc/profile.d/rvm.sh ;\
  sed -i "4i source /etc/profile.d/rvm.sh" /root/.bashrc ;\
  \
  echo "# Installing Ruby 2.1.2" ;\
  rvm install 2.1.2 ;\
  gem install bundler --no-ri --no-redoc ;\
  \
  echo "# Install ImageMagick" ;\
  apt-get install -q -y imagemagick libmagickwand-dev ;\
  \
  echo "# Cleaning up" ;\
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /setup /build ;\
  true'
# END RUN
