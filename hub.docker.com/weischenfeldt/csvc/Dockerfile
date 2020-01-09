FROM centos:7.3.1611

# File Author / Maintainer
LABEL maintainer="francesco.favero@bric.ku.dk"

# Set versions
ENV PERL_VERSION 5.18.4
ENV HTSLIB_VERSION 1.9
ENV SAMTOOLS_VERSION 1.9
ENV BEDTOOLS_VERSION 2.22.1
ENV BIGWIG_VERSION 1.0.2
ENV KENT_VERSION 334


## Setup packages
USER root
RUN yum install -y epel-release

# Install base software
RUN yum install -y wget  gcc gcc-c++ make cmake lsof \
    bzip2 libdb-devel gd-devel openssl openssl-devel ncurses-devel \
    libcurl-devel gnutls-devel sqlite-devel glibc-devel patch expat-devel \
    libtasn1-devel p11-kit-devel gmp-devel nettle-devel time python-devel \
    python-pip


# Install perl
RUN wget http://www.cpan.org/src/5.0/perl-$PERL_VERSION.tar.gz \
    && tar -xzf perl-$PERL_VERSION.tar.gz \
    && cd perl-$PERL_VERSION && ./Configure -des -Dprefix=/usr/local \
    && make && make install && cd ../ \
    && rm -rf perl-$PERL_VERSION.tar.gz perl-$PERL_VERSION

# Install cpanm
RUN PERL_MM_USE_DEFAULT=1 PERL_EXTUTILS_AUTOINSTALL="--defaultdeps" cpan -i App::cpanminus

# Install bioinformatics software
RUN yum install -y R bwa

# Install Samtools
RUN wget https://github.com/samtools/samtools/releases/download/$SAMTOOLS_VERSION/samtools-$SAMTOOLS_VERSION.tar.bz2 -O samtools.tar.bz2 \
    && tar -xjvf samtools.tar.bz2 &&  cd samtools-$SAMTOOLS_VERSION \
    && make CXXFLAGS=-fPIC CFLAGS=-fPIC CPPFLAGS=-fPIC && make prefix=/usr/local install \
    && cd ../ && rm -rf samtools-$SAMTOOLS_VERSION samtools.tar.bz2


# Install BEDtools
RUN wget https://github.com/arq5x/bedtools2/releases/download/v$BEDTOOLS_VERSION/bedtools-$BEDTOOLS_VERSION.tar.gz -O bedtools.tar.gz \
    && tar -xvf bedtools.tar.gz &&  cd bedtools2 \
    && make CXXFLAGS=-fPIC CFLAGS=-fPIC CPPFLAGS=-fPIC && make prefix=/usr/local install \
    && cd ../ && rm -rf bedtools2 bedtools.tar.gz


# Install cgpBigWig
RUN wget https://github.com/cancerit/cgpBigWig/archive/$BIGWIG_VERSION.tar.gz -O bigwig.tar.gz \
    && tar -zxf bigwig.tar.gz &&  cd cgpBigWig-$BIGWIG_VERSION/ \
    && ./setup.sh /usr/local \
    && cd ../ && rm -rf bigwig.tar.gz cgpBigWig-$BIGWIG_VERSION

# Install Biobambam
RUN wget https://github.com/gt1/biobambam2/releases/download/2.0.54-release-20160802163650/biobambam2-2.0.54-release-20160802163650-x86_64-etch-linux-gnu.tar.gz -O biobambam2.tar.gz \
    && mkdir -p biobambam2 \
    && tar --strip-components 1 -C biobambam2 -zxf biobambam2.tar.gz \
    && mkdir -p /usr/local/bin /usr/local/etc /usr/local/lib /usr/local/share \
    && rm -f biobambam2/bin/curl \
    && cp -r biobambam2/bin/* /usr/local/bin/ \
    && cp -r biobambam2/etc/* /usr/local/etc/ \
    && cp -r biobambam2/lib/* /usr/local/lib/ \
    && cp -r biobambam2/share/* /usr/local/share/ \
    && rm -rf biobambam2  biobambam2.tar.gz

# Install perl module and add local *.pm to the perl installation
RUN cpanm install IPC::System::Simple Math::Combinatorics \
    File::ShareDir::Install List::Util LWP::Protocol::https \
    File::ShareDir DBD::SQLite XML::SAX::Expat PPI::HTML \
    Config::IniFiles Bio::Tools::Run::WrapperBase DateTime Bio::Perl

## Copy and install required Perl modules
ADD PerlSvAnalysisLib/ /PerlSvAnalysisLib
ADD BRASS/ /BRASS
# Install HTSlib first (needs to be here for some reason)
RUN wget https://github.com/samtools/htslib/releases/download/$HTSLIB_VERSION/htslib-$HTSLIB_VERSION.tar.bz2 -O htslib.tar.bz2 \
    && tar -xjvf htslib.tar.bz2 \
    && cd htslib-$HTSLIB_VERSION && ./configure \
    && make CXXFLAGS=-fPIC CFLAGS=-fPIC CPPFLAGS=-fPIC && make install \
    && cd ../ && rm -rf htslib-$HTSLIB_VERSION htslib.tar.bz2 \
    && cpanm install Bio::DB::HTS::Tabix \
    && cp /PerlSvAnalysisLib/*.pm /usr/local/lib/perl5/site_perl/$PERL_VERSION/ \
    && cp /PerlSvAnalysisLib/*.pl /usr/local/bin && chmod +x /usr/local/bin/*.pl \
    && rm -rf /PerlSvAnalysisLib

# Download and setup kent sources
ENV MACHTYPE i686
ENV KENT_SRC /kent-$KENT_VERSION\_base/src
RUN wget https://github.com/ucscGenomeBrowser/kent/archive/v$KENT_VERSION\_base.tar.gz -O kent.tar.gz \
    && tar -zxf kent.tar.gz && cd /kent-$KENT_VERSION\_base/src/lib \
    && make CXXFLAGS=-fPIC CFLAGS=-fPIC CPPFLAGS=-fPIC \
    && cpanm install Bio::DB::BigWig \
    && cd / && rm -rf kent.tar.gz /kent-$KENT_VERSION\_base

RUN cpanm install https://github.com/ICGC-TCGA-PanCancer/PCAP-core/archive/v3.5.0.tar.gz \
    && cpanm install /BRASS/perl && rm -rf /BRASS/

# Install R and python packages

ADD install_files/py_requirements.txt /root/py_requirements.txt

# numpy needs to be installed first otherwise pandas cannot be installed
RUN pip install numpy==1.11.1 && pip install --no-cache-dir -r /root/py_requirements.txt \
    && rm /root/py_requirements.txt

## Install R requirements in system libs

ADD install_files/r_requirements.Rscript /root/r_requirements.Rscript
RUN Rscript /root/r_requirements.Rscript && rm /root/r_requirements.Rscript

ADD run_pipeline.py /usr/local/bin/run_csvc.py
ADD run_pipeline_fast.py /usr/local/bin/run_csvc_fast.py

## Install pype modules
ADD pype_modules/repos.yaml /root/repos.yaml
RUN pype repos -r /root/repos.yaml install -f csvc \
    && chmod +x /usr/local/bin/run_csvc.py \
    && chmod +x /usr/local/bin/run_csvc_fast.py \
    && rm /root/repos.yaml \
    && mkdir /databases && chmod -R 7777 /databases \
    && mkdir /data && chmod -R 7777 /data

ADD r_scripts /opt/Rscripts

ADD sv_covplot /root/sv_covplot
RUN chmod +x /root/sv_covplot/bin/* \
    && mv /root/sv_covplot/bin/* /usr/local/bin/ \
    && rm -rf /root/sv_covplot

VOLUME /databases /data

RUN useradd -ms /bin/bash  docker \
    && yum clean all -q \
	&& rm -fr /var/cache/yum/* /tmp/* /var/tmp/* /root/.pki

USER docker

WORKDIR /home/docker

CMD ["/bin/bash"]
