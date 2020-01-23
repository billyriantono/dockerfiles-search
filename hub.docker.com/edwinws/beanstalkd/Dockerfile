FROM debian:wheezy
LABEL maintainer="Edwin William Sieh <william.edwinx@gmail.com>"

ADD install.sh install.sh
RUN chmod +x install.sh; sync; ./install.sh; rm install.sh

EXPOSE 11300
CMD ["beanstalkd", "-p", "11300", "-z", "10485760"]
