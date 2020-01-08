FROM gitlab/gitlab-ce:12.0.3-ce.0
ENV DATA 1578232315_2020_01_05_12.0.3
COPY wrapper /assets/wrapper
COPY gitlab.rb /opt/gitlab/etc/gitlab.rb.template
COPY gitlab-secrets.json /tmp
COPY ${DATA}_gitlab_backup.tar /tmp
COPY poll-complete.sh /poll-complete.sh
RUN chmod 766 /assets/wrapper
RUN chmod 755 /poll-complete.sh