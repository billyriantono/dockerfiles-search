FROM istepanov/dokuwiki

RUN apk --no-cache add unzip

RUN curl -o jbcrawford-ng.zip -L "https://github.com/jcrawfordor/jbcrawford-ng/archive/master.zip" && \
    unzip jbcrawford-ng.zip -d /var/www/lib/tpl/ && \
    mv /var/www/lib/tpl/jbcrawford-ng-master /var/www/lib/tpl/jbcrawford-ng && \
    rm -rf jbcrawford-ng.zip
RUN curl -o dokuwiki-plugin-bootswrapper.zip -L "https://github.com/LotarProject/dokuwiki-plugin-bootswrapper/archive/master.zip" && \
    unzip dokuwiki-plugin-bootswrapper.zip -d /var/www/lib/plugins/ && \
    mv /var/www/lib/plugins/dokuwiki-plugin-bootswrapper-master /var/www/lib/plugins/bootswrapper && \
    rm -rf dokuwiki-plugin-bootswrapper.zip
