FROM digitalcz/apache2

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository -y ppa:ondrej/php

RUN apt-get update && apt-get install -y --allow-unauthenticated php5.6 libapache2-mod-php5.6