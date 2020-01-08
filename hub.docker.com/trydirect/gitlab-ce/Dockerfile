FROM gitlab/gitlab-ce:11.8.2-ce.0
RUN apt-get update -y -qq; apt-get install -y -qq nginx supervisor; mkdir -p /opt/letsencrypt;

ADD ./scripts/letsencrypt-auto /opt/letsencrypt/letsencrypt-auto
RUN chmod +x /opt/letsencrypt/letsencrypt-auto; /opt/letsencrypt/letsencrypt-auto  --os-packages-only --install-only --non-interactive

RUN  apt-get clean; apt-get autoclean; apt-get autoremove -y -qq;
RUN groupadd -r -g 2000 gitlab; useradd -r -u 2000 -g 2000 -m -c "app account" -d /home/gitlab -s /bin/bash gitlab
