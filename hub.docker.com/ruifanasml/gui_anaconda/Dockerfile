FROM ruifanasml/guibase

ADD install/anaconda.sh $INST_SCRIPTS/anaconda.sh
RUN chmod +x $INST_SCRIPTS/anaconda.sh && $INST_SCRIPTS/anaconda.sh
ENV PATH /usr/local/anaconda2/bin:$PATH
RUN yum -y install git \
    yum -y install sssd \
  && yum clean all
