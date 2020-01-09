FROM ubuntu:14.04
MAINTAINER igronemyk<igronemyk@gmail.com>, billchenchina<billchenchina2001@gmail.com>
RUN apt-get -qq update -y && apt-get -qq install -y git wget && cd ~ && git clone https://github.com/universaloj-test/install-scripts --depth=1 && bash install-scripts/install.sh
EXPOSE 80 3690
CMD /root/up
