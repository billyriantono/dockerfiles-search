FROM templateria/tsuru-base

# reusing base image scripts
RUN ln -s /var/lib/tsuru/base/start /var/lib/tsuru/start
RUN ln -s /var/lib/tsuru/base/restart /var/lib/tsuru/restart

# using our own scripts
ADD scripts/setup   /var/lib/tsuru/setup
ADD scripts/deploy  /var/lib/tsuru/deploy
ADD scripts/install /var/lib/tsuru/install
ADD scripts/create_fpm_envs.py /var/lib/tsuru/create_fpm_envs.py
ADD scripts/php5-fpm        /var/lib/tsuru/php5-fpm

ADD configs            /var/lib/tsuru/configs

RUN /var/lib/tsuru/install
RUN /var/lib/tsuru/setup
