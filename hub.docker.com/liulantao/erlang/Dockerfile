# VERSION v1
# docker build -t="liulantao/erlang:v3" .
FROM liulantao/fpm
MAINTAINER Liu Lantao <liulantao@gmail.com>
ENV REFRESHED_AT 2016-08-25
RUN curl http://packages.erlang-solutions.com/rpm/centos/erlang_solutions.repo -o /etc/yum.repos.d/erlang_solutions.repo && \
yum install -yq erlang git expat-devel redhat-lsb-core && yum clean all
