FROM centos:centos7

RUN yum install -y  https://centos7.iuscommunity.org/ius-release.rpm \
    && yum -y update \
    && yum install -y python36u python36u-libs python36u-devel python36u-pip 

RUN pip3.6 install -U numpy pandas scipy scikit-learn matplotlib seaborn plotly

#CMD ["bash"]
