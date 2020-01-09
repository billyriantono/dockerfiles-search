FROM fedora:28
RUN curl -o /etc/yum.repos.d/fedora.repo http://mirrors.aliyun.com/repo/fedora.repo &&\
  curl -o /etc/yum.repos.d/fedora-updates.repo http://mirrors.aliyun.com/repo/fedora-updates.repo &&\
  dnf makecache &&\
  dnf install gcc-c++ -y &&\
  dnf install golang -y &&\
  dnf install cmake -y &&\
  dnf install git -y &&\
  mkdir /root/go &&\
  mkdir /root/cpp &&\
  echo "export GOPATH=/root/go" >> /root/.bashrc &&\
  echo 'export PATH=${PATH}:${GOPATH}/bin' >> /root/.bashrc