FROM perl
MAINTAINER hezengliang hezengliang@gmail.com
RUN apt-get update && apt-get install --force-yes -y expat libexpat1-dev
WORKDIR /usr/src/myapp
ADD ./cpanfile /root/
ADD ./cpanm /bin/
CMD cd ~ && /bin/cpanm --installdeps .
