FROM ubuntu:18.04

RUN  apt-get update && \
     apt-get install -y language-pack-ru mc && \
     apt-get install -y  dh-make-perl && \
     apt-get install -y apt-file && \
     apt-get clean
RUN apt-get -y install sudo
# зависимости для ST/Common
RUN  apt-get install -y libclass-factory-perl libdbi-perl libcache-cache-perl
# зависимости для ST/Reports
RUN apt-get install -y libdbd-xbase-perl libspreadsheet-writeexcel-perl libexcel-writer-xlsx-perl
# зависимости для ST/Loader
RUN apt-get install -y libfile-touch-perl


# Set environment variables.
ENV LANG ru_RU.UTF-8
#ENV HOME /home/cpn
ENV DISPLAY :0
ENV VERSION 1.0.0

# Define working directory.
WORKDIR /home/dev
RUN git config --global user.email "you@example.com"
RUN git config --global user.name "Ваше Имя"

ADD entrypoint.sh /bin/entrypoint.sh
ENTRYPOINT ["/bin/entrypoint.sh"]
