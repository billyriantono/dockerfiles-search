FROM gitlab/gitlab-ce

RUN (mv /etc/localtime /etc/localtime.old; ln -s /usr/share/zoneinfo/Asia/Bangkok /etc/localtime)
#RUN useradd -ms /bin/bash ubuntu

RUN apt-get update && apt-get install software-properties-common -y --allow-unauthenticated
RUN add-apt-repository ppa:certbot/certbot -y
RUN apt-get update && apt-get install certbot -y --allow-unauthenticated
