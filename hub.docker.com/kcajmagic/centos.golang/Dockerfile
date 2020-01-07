FROM centos:7

RUN yum install -y golang make git epel-release rpm-build rpmdevtools && rpmdev-setuptree
RUN rpm --import https://mirror.go-repo.io/centos/RPM-GPG-KEY-GO-REPO
RUN curl -s https://mirror.go-repo.io/centos/go-repo.repo | tee /etc/yum.repos.d/go-repo.repo
RUN yum install -y golang
RUN yum clean all
RUN mkdir -p /go/bin
ENV GOPATH /go
ENV GOBIN /go/bin
ENV PATH $PATH:$GOBIN
