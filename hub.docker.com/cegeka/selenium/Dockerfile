FROM selenium/standalone-chrome-debug:3.6.0-bromine
USER root
#=================
# Locale settings
#=================
ENV LANGUAGE nl_BE.UTF-8
ENV LANG nl_BE.UTF-8
RUN locale-gen nl_BE.UTF-8 \
  && dpkg-reconfigure --frontend noninteractive locales \
  && apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    language-pack-en \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

USER seluser