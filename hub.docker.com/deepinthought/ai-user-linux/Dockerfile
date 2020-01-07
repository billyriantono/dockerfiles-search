FROM ubuntu:bionic
RUN  apt-get update \
  && apt-get install -y wget curl net-tools \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p /dbc-ai-user;

MAINTAINER Luke P. @ DeepInThought

SHELL [ "/bin/bash", "-c" ]
WORKDIR /dbc-ai-user
# DeepBrainChain AI User Install
ARG AI_USER_LINUX_INSTALL=ai_user_linux_install.sh 
ARG AI_USER_LINUX_INSTALL_SHA512SUM=6dc207c38aaf2b7976f827035fe3ea2abd91d366d245a09c695533b817f7675e19dab67927af8f5158855d1fd226a0d44ac01202f774b19e06162842db71a0f5
ARG ai_user_linux_install_url="https://github.com/DeepBrainChain/deepbrainchain-release/releases/download/latest/${AI_USER_LINUX_INSTALL}"
# Grab the latest ai_user_linux_install.sh script and verify it's sha512sum is valid \
RUN wget -O ${AI_USER_LINUX_INSTALL} "$ai_user_linux_install_url"; \
  echo "${AI_USER_LINUX_INSTALL_SHA512SUM}  ${AI_USER_LINUX_INSTALL}" | sha512sum -c - || exit 1;
  
# Add Client Release Package & fix the ai_user_linux_install.sh to verify with sha512sum -c.
ARG release_version=0.3.4.1
ARG DBC_LINUX_CLIENT_RELEASE_PACKAGE=dbc-linux-client-${release_version}.tar.gz 
ARG DBC_LINUX_CLIENT_RELEASE_PACKAGE_SHA512SUM=cf1d2b354cfd1626f6ee52236bff24ab1580f7e47b1e158067d1adb54da81b4ccd9bb261ffd5ed0de35591e4d377522cd2bc20cb0f03db5ba5bfd6a3c6955f93 
ARG dbc_linux_client_url="https://github.com/DeepBrainChain/deepbrainchain-release/releases/download/latest/dbc-linux-client-${release_version}.tar.gz"
RUN sed -i 's|release_version=.*|release_version='${release_version}'|g' "${AI_USER_LINUX_INSTALL}"; \
  sed -i 's|wget https.*|wget -O '${DBC_LINUX_CLIENT_RELEASE_PACKAGE}' '${dbc_linux_client_url}' \;|g' "${AI_USER_LINUX_INSTALL}"; \
  sed -i '/wget -O/ s/$/echo "'${DBC_LINUX_CLIENT_RELEASE_PACKAGE_SHA512SUM}'  '${DBC_LINUX_CLIENT_RELEASE_PACKAGE}'" \| sha512sum \-c \- \|\| exit 1\;/' "${AI_USER_LINUX_INSTALL}"; \
  source ai_user_linux_install.sh; \
  apt-get remove -y wget curl net-tools  \
  && apt autoclean \
  && apt autoremove -y; 
  
CMD [ "/dbc-ai-user/0.3.4.1/dbc_repo/dbc" ]

LABEL email="support@deepinthought.io" Author="Luke P. @ DeepInThought"