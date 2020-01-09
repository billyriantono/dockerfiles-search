FROM liyustar/sshd
MAINTAINER liyustar <liyustar@gmail.com>

# RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y g++
RUN apt-get install -y libboost-all-dev
RUN apt-get install -y vim

# 下载Boost
# RUN wget http://kent.dl.sourceforge.net/project/boost/boost/1.57.0/boost_1_57_0.tar.bz2 -o boost_1_57_0.tar.bz2 && \
#         tar jxf boost_1_57_0.tar.bz2 -C . && \
#         rm -rf boost_1_57_0.tar.bz2
# 编译Boost


# Declare
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
