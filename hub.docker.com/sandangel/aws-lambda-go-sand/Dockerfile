FROM eawsy/aws-lambda-go-shim

RUN true \
  && yum -q -e 0 -y update || true \
  && yum -q -e 0 -y install aws-cli git || true \
  && yum -q -e 0 -y clean all
