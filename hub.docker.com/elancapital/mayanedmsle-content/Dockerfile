FROM centos:7

WORKDIR /tmp

COPY . /

# install zip
RUN yum -y install unzip

# install wget
RUN yum -y install wget

# install sudo
RUN yum -y install sudo 

# install tee
# RUN sudo rpm -i tee

# download & install bcl2fastq
RUN curl -o bcl2fastq.zip https://support.illumina.com/content/dam/illumina-support/documents/downloads/software/bcl2fastq/bcl2fastq2-v2-20-0-linux-x86-64.zip \
    && unzip bcl2fastq.zip \
    && rpm -i bcl2fastq*rpm

# download and install gsutil (https://cloud.google.com/storage/docs/gsutil_install#linux)
RUN source /gcloud_sdk_command.txt

RUN yum -y install google-cloud-sdk
