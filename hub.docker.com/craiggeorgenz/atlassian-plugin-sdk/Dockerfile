FROM ubuntu:19.10

RUN apt-get update -y; \
  apt install openjdk-8-jdk wget gnupg -y; \
  sh -c 'echo "deb https://packages.atlassian.com/atlassian-sdk-deb stable contrib" >>/etc/apt/sources.list'; \
  wget https://packages.atlassian.com/api/gpg/key/public; \
  apt-key add public; \
  apt-get update -y; \
  apt-get install atlassian-plugin-sdk=8.0.16; \
  atlas-version --help; \
