FROM bodom0015/xpra-base:fix-pycharm-2017

RUN yum update -q -y && \
    yum install -q -y \
        python-pip && \ 
    yum autoremove -q -y && \
    yum clean all -q -y

# install PyCharm
RUN wget -q http://download.jetbrains.com/python/pycharm-community-2017.2.tar.gz && \
    tar xvfz pycharm-community-2017.2.tar.gz && \ 
    rm pycharm-community-2017.2.tar.gz 

COPY entrypoint.sh /

