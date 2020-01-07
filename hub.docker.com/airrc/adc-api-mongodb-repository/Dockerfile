# Base MongoDB image
FROM mongo:3

LABEL maintainer="Scott Christley <scott.christley@utsouthwestern.edu>"

# You might want to run mongodb as a specific user (versus root),
# particularly so that it has access to host directories. You need to
# create that user and group within the docker container with the same
# user and group identifiers as on the host system. Uncomment and
# modify the following lines accordingly.

# setup airr user/group
#RUN echo "airr:x:123456:56789:AIRR User,,,:/home/airr:/bin/bash" >> /etc/passwd
#RUN echo "airr:x:56789:airr" >> /etc/group
#RUN mkdir /home/airr
#RUN chown airr /home/airr
#RUN chgrp airr /home/airr
#USER airr
