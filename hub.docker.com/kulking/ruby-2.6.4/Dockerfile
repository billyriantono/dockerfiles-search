FROM ubuntu:18.04
RUN cd /home; \
apt-get -y update; \
apt-get install -y autoconf build-essential libreadline-dev libssl-dev libyaml-dev zlib1g-dev libffi-dev wget; \
wget https://cache.ruby-lang.org/pub/ruby/2.6/ruby-2.6.4.tar.gz; \
gunzip -c ruby-2.6.4.tar.gz | tar xopf -; \
cd ruby-2.6.4; \
./configure; make; make install; \
rm -rf /home/ruby-2.6.4/; \
rm /home/ruby-2.6.4.tar.gz; \
cd ~