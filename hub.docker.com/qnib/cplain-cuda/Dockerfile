FROM qnib/cplain-init:7.4.1708

RUN rpm -i http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
 && rpm -i http://us.download.nvidia.com/tesla/390.30/nvidia-diag-driver-local-repo-rhel7-390.30-1.0-1.x86_64.rpm \
 && yum clean all \
 && yum install -y cuda-drivers
