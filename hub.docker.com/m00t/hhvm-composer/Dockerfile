FROM m00t/hhvm

MAINTAINER Anton Serdyuk <anton.serdyuk@gmail.com>

RUN wget https://getcomposer.org/installer -O installer.php
RUN hhvm -v Http.SlowQueryThreshold=30000 -v ResourceLimit.SocketDefaultTimeout=30 -v Eval.Jit=false installer.php --install-dir=/opt --filename=composer.phar
RUN rm installer.php
ADD composer /usr/local/bin/