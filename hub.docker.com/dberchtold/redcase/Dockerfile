FROM redmine:3.3.0
MAINTAINER dietmar.berchtold@anecon.at

COPY migration.sh /usr/src/redmine/

RUN apt-get update \
    && apt-get install unzip \
    && curl -L https://bitbucket.org/bugzinga/redcase/downloads/redcase-1.0.zip --out /tmp/redcase-1.0.zip \
    && unzip /tmp/redcase-1.0.zip -d /usr/src/redmine/plugins \
    && sed -i 's/null => false/null => true/' /usr/src/redmine/plugins/redcase/db/migrate/004_redcase_patch_journal.rb \
    && chmod +x /usr/src/redmine/migration.sh \
    && /usr/src/redmine/migration.sh



