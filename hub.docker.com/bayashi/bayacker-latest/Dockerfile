# 1. Container should be ephemeral.
# 2. Don't install unnecessary packages.
# 3. Each container should have only one application.
# 4. Sorting multi-line arguments alphanumerically.
# 5. Installing something, show version immediately

FROM bayashi/bayacker:0.06

MAINTAINER bayashi

ENTRYPOINT ["/bin/bash"]

ENV MY_USER bayashi
ENV MY_HOME /home/bayashi
ENV PERL_DIR /perl5
ENV PERL_VERSION 5.28.1
ENV PATH $MY_HOME/${PERL_DIR}-${PERL_VERSION}/bin:$PATH

# Perl
RUN curl -sL https://raw.githubusercontent.com/tokuhirom/Perl-Build/master/perl-build > $MY_HOME/bin/perl-build
RUN perl -pi -e 's%^#!/usr/bin/env perl%#!/usr/bin/perl%g' $MY_HOME/bin/perl-build
RUN chmod +x $MY_HOME/bin/perl-build
RUN mkdir $MY_HOME/${PERL_DIR}-${PERL_VERSION} \
&& chown $MY_USER:$MY_USER $MY_HOME/${PERL_DIR}-${PERL_VERSION}
RUN perl-build $PERL_VERSION $MY_HOME/${PERL_DIR}-${PERL_VERSION}
RUN curl -sL http://cpanmin.us/ | $MY_HOME/${PERL_DIR}-${PERL_VERSION}/bin/perl - --notest App::cpanminus Carton

RUN cpanm --notest Plack

# daemontools for envdir
# https://github.com/kteru/daemontools-rpm
#COPY daemontools-toaster-0.76-1.3.6.x86_64.rpm ./
#RUN sudo rpm -ivh daemontools-toaster-0.76-1.3.6.x86_64.rpm \
#&& rm -f ./daemontools-toaster-0.76-1.3.6.x86_64.rpm
