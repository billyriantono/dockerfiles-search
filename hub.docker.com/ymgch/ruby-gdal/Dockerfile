# FROM ruby:2.4
#
# RUN set -x \
# && apt-key adv --keyserver keys.gnupg.net --recv-key 'E19F5F87128899B192B1A2C2AD5F960A256A04AF' \
# && sed -i -e 's/deb.debian.org/cdn.debian.net/g' /etc/apt/sources.list \
# && echo 'deb http://cran.ism.ac.jp/bin/linux/debian jessie-cran34/' >> /etc/apt/sources.list \
# && apt-get -qq update && apt-get install -y -qq r-base libgdal-dev libproj-dev \
# && rm -rf /var/lib/apt/lists/* \
# && R --vanilla --slave -e 'install.packages(c("gstat", "rgdal"), repos="http://cran.ism.ac.jp/")'

FROM ruby:2.5

RUN set -x \
&& sed -i -e 's/deb.debian.org/cdn.debian.net/g' /etc/apt/sources.list \
&& apt-get -qq update && apt-get install -y -qq r-base libgdal-dev libproj-dev \
&& rm -rf /var/lib/apt/lists/* \
&& R --vanilla --slave -e 'install.packages(c("gstat", "rgdal"), repos="http://cran.ism.ac.jp/")'
