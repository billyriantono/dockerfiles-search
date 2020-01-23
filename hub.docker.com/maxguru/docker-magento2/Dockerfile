FROM alexcheng/magento2

RUN apt-get update \
&& apt-get upgrade -yq --no-install-recommends --no-install-suggests \
&& apt-get install -yq --no-install-recommends --no-install-suggests ssmtp sudo mysql-client \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
