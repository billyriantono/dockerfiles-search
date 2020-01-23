#Chris Green
#goland builder

FROM golang:1.11 as go_builder

COPY . /go/src/github.com/malice-plugins/sophos
WORKDIR /go/src/github.com/malice-plugins/sophos
RUN go get -u github.com/golang/dep/cmd/dep && dep ensure
RUN go build -ldflags "-s -w -X main.Version=v$(cat VERSION) -X main.BuildTime=$(date -u +%Y%m%d)" -o /bin/avscan

#Sophos Dockerfile

FROM centos:7

LABEL maintainer "https://github.com/blacktop"

LABEL malice.plugin.repository = "https://github.com/malice-plugins/sophos.git"
LABEL malice.plugin.category="av"
LABEL malice.plugin.mime="*"
LABEL malice.plugin.docker.engine="*"

# Create a malice user and group first so the IDs get set the same way, even as
# the rest of this may change over time.
RUN groupadd -r malice \
  && useradd --no-log-init -r -g malice malice \
  && mkdir /malware \
  && chown -R malice:malice /malware

#Packages needed 
#RUN rpm --import http://download.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 \
RUN yum -y install epel-release \
&& yum -y update \
#&& yum -y install clamav-data-empty clamav-update \
&& yum -y install wget \
&& yum clean all
RUN mkdir -p /tmp
WORKDIR /tmp
# Download Sophos
RUN buildDeps='ca-certificates wget' \
&& yum update -qq \
&& yum install -yq $buildDeps \
&& echo "Install Sophos..." \
&& cd /tmp \
&& wget https://github.com/maliceio/malice-av/raw/master/sophos/sav-linux-free-9.tgz \
&& tar xzvf sav-linux-free-9.tgz \
&& ./sophos-av/install.sh /opt/sophos --update-free --acceptlicence --autostart=False --enableOnBoot=False --automatic --ignore-existing-installation --update-source-type=s \
&& echo "Clean up unnecessary files..." \
#&& yum purge -y --auto-remove $buildDeps \
#&& yum clean \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /go

COPY --from=go_builder /bin/avscan /bin/avscan
# Update Sophos
RUN /opt/sophos/update/savupdate.sh
# Add EICAR Test Virus File to malware folder
ADD http://www.eicar.org/download/eicar.com.txt /malware/EICAR
WORKDIR /malware
ENTRYPOINT ["/bin/avscan"]
CMD ["--help"]
