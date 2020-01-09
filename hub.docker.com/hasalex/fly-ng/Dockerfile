FROM sewatech/apache

RUN apt-get update && apt-get install -y curl &&\
    rm -r /var/www/html/* &&\
    (curl -skL https://bintray.com/artifact/download/hasalex/generic/fly-ng.tar.gz | tar xfz - -C /var/www/html/)
