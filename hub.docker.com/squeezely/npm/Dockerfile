FROM squeezely/phpcli:latest

COPY wait-for-it.sh /root/wait-for-it.sh

RUN chmod a+x /root/wait-for-it.sh
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
