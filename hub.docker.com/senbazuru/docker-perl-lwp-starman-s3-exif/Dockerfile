FROM senbazuru/docker-perl
MAINTAINER senbazuru
# see also
# https://github.com/DQNEO/docker-perllwp
# https://github.com/DQNEO/docker-perllwpstarman
# https://github.com/DQNEO/docker-perllwpstarmans3exif

RUN /usr/bin/yum install -y openssl openssl-devel
RUN yum clean all

#install cpan module
RUN cpanm URI HTTP::Date HTTP::Request HTTP::Response HTTP::Status Net::HTTP
RUN cpanm LWP::UserAgent
RUN cpanm HTTP::Body@1.19
RUN cpanm Plack
RUN cpanm Starman
RUN cpanm Image::ExifTool
RUN cpanm JSON::XS
RUN cpanm Config::Tiny
RUN cpanm Amazon::S3::Thin
RUN cpanm Class::Accessor::Fast # remove this in future
#clean temp
RUN  rm -rf /root/.cpanm/work/*

