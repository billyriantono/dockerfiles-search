FROM centos:centos7

RUN yum install -y epel-release
RUN yum install -y libgcrypt-devel
RUN yum install -y unzip
RUN yum install -y libxslt
RUN yum install -y libxslt-devel
RUN yum install -y gcc-c++
RUN yum install -y ImageMagick
RUN yum install -y bzip2
RUN yum install -y bzip2-devel
RUN yum install -y zlib
RUN yum install -y zlib-devel
RUN yum --enablerepo=epel install -y  	mingw64-boost
RUN yum install -y libxml2
RUN yum install -y libxml2-devel

# Install bcl2fastq 2.20.0
ADD https://support.illumina.com/content/dam/illumina-support/documents/downloads/software/bcl2fastq/bcl2fastq2-v2-20-0-linux-x86-64.zip /

RUN unzip /bcl2fastq2-v2-20-0-linux-x86-64.zip && \
	rpm -i bcl2fastq2-v2.20.0.422-Linux-x86_64.rpm && \
	rm /bcl2fastq2-v2-20-0-linux-x86-64.zip && \
	rm /bcl2fastq2-v2.20.0.422-Linux-x86_64.rpm


