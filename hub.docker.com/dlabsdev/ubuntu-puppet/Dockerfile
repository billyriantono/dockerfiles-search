FROM ubuntu:14.04

MAINTAINER Leo Schweizer <leonhard.schweizer@gmail.com>

RUN \
  apt-get update && \
  apt-get --yes install git wget

RUN \
  repo_deb_path=$(mktemp) && \
  wget --output-document="${repo_deb_path}" "https://apt.puppetlabs.com/puppetlabs-release-pc1-wheezy.deb" && \
  dpkg -i "${repo_deb_path}" && \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" install puppet-agent
