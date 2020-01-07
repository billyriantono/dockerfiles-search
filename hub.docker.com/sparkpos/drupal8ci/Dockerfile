FROM juampynr/drupal8ci

RUN apt-get update -y && apt-get install openssh-client -y
RUN mkdir /root/.ssh
ADD spark_deploy.key /root/.ssh/id_rsa
ADD spark_deploy.pub /root/.ssh/id_rsa.pub
ADD ssh-config /root/.ssh/config

RUN chmod 400 /root/.ssh/id_rsa

RUN docker-php-ext-install bcmath
