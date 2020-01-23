FROM nvidia/caffe
MAINTAINER pearson@illinois.edu

ADD setuser.sh /setuser.sh
ADD runas.sh /runas.sh 

ENTRYPOINT ["/runas.sh"]
