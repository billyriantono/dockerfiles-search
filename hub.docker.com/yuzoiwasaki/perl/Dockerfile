# base image
FROM centos:7
MAINTAINER Yuzo Iwasaki

# color definition
ENV NORMAL \e[0;39m
ENV SUCCESS \e[0;32m
ENV FAIL \e[0;31m

# git install check
RUN if [ ! $(type -P git) ] > /dev/null 2>&1; then yum -y install git; fi
# tar install check
RUN if [ ! $(type -P tar) ] > /dev/null 2>&1; then yum -y install tar; fi
# gcc install check
RUN if [ ! $(type -P gcc) ] > /dev/null 2>&1; then yum -y install gcc; fi

# install plenv
RUN git clone git://github.com/tokuhirom/plenv.git ~/.plenv
RUN git clone git://github.com/tokuhirom/Perl-Build.git ~/.plenv/plugins/perl-build/
ENV PATH /root/.plenv/bin:$PATH
RUN echo 'eval "$(plenv init -)"' >> ~/.bash_profile
RUN if [ ! $(type -P plenv) ] > /dev/null 2>&1; then echo -e "${FAIL}plenv installation failed !${NORMAL}"; else echo -e "${SUCCESS}plenv was installed successfully.${NORMAL}"; fi

# install cpanm
RUN yum -y install cpanminus
RUN if [ ! $(type -P cpanm) ] > /dev/null 2>&1; then echo -e "${FAIL}cpanm installation failed !${NORMAL}"; else echo -e "${SUCCESS}cpanm was installed successfully.${NORMAL}"; fi

# install carton
RUN cpanm Test::More
RUN cpanm Carton
RUN if [ ! $(type -P carton) ] > /dev/null 2>&1; then echo -e "${FAIL}Carton installation failed !${NORMAL}"; else echo -e "${SUCCESS}Carton was installed successfully.${NORMAL}"; fi

# install common modules
RUN modules=("DBI" "Data::Dumper" "DateTime" "Encode" "Getopt::Long"); \
    for module in ${modules[@]}; do \
      if cpanm $module; then \
        echo -e "${SUCCESS}$_ was installed successfully.${NORMAL}"; \
      else \
        echo -e "${FAIL}$_ installation failed !${NORMAL}"; \
      fi \
    done;

# install Plack
RUN cpanm Plack

# install Mojolicious
RUN if [ ! $(type -P perl-Time-HiRes) ] > /dev/null 2>&1; then yum -y install perl-Time-HiRes; fi
RUN cpanm Mojolicious

RUN yum clean all

ENV WELCOME_MSG -----------------------------------------\n\
\tWelcome to Perl World !\n\
-----------------------------------------

RUN echo -e $WELCOME_MSG
