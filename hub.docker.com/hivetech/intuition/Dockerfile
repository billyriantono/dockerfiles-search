# hivetech/intuition image
# A raring box with Intuition (https://github.com/hackliff/intuition installed
# and ready to use
#   docker run \
#     -e DB_HOST=172.17.0.4 \
#     -e LANG=fr_FR.UTF-8 \
#     -e LOG=info \
#     -e QUANDL_API_KEY=$QUANDL_API_KEY \
#     hivetech/intuition --context insights.contexts.mongodb.MongodbContext://192.168.0.19:27017/intuition/contexts/bt-yahoo --id chuck --bot --showlog
# VERSION 0.1.0

# Administration
# hivetech/pyscience is an ubuntu 12.04 image with most popular python packages
FROM hivetech/pyscience
MAINTAINER Xavier Bruhiere <xavier.bruhiere@gmail.com>

# Local settings
#RUN apt-get update && \
  #apt-get install -y language-pack-fr wget git-core libssl-dev
#ENV LANGUAGE fr_FR.UTF-8
#ENV LANG fr_FR.UTF-8
#ENV LC_ALL fr_FR.UTF-8
#RUN locale-gen fr_FR.UTF-8 && dpkg-reconfigure locales

RUN git clone https://github.com/intuition-io/intuition.git -b develop --depth 1 && \
  cd /intuition && python setup.py install

# Install modules
RUN git clone https://github.com/intuition-io/insights.git -b develop --depth 1 && \
  apt-get update && apt-get install -y libreadline-dev && \
  cd insights && python setup.py install
# Install R libraries
RUN wget -qO- http://bit.ly/L39jeY | R --no-save

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["/usr/local/bin/intuition", "--showlog"]
CMD ["--help"]
