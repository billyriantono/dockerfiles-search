
FROM rails:onbuild

# Need this since Docker's RUN commands call /bin/sh and /bin/sh doesn't support source to/some/path/exec
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

WORKDIR /usr/src/app
RUN cp database.yml.aws config/database.yml
RUN chmod 700 start.sh
RUN chmod 700 provision.sh
RUN chmod 700 worker.sh
EXPOSE 3000
