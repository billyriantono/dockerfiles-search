FROM cloudpack/openssh

RUN yum -y update
RUN yum -y install vim git epel-release
RUN yum -y install python-pip
RUN yum -y clean all
RUN pip install awscli

RUN echo >> /root/.bash_profile
RUN echo 'complete -C aws_completer aws' >> /root/.bash_profile
RUN echo 'export AWS_DEFAULT_REGION=`curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone | sed -e "s/.$//"`' >> /root/.bash_profile

