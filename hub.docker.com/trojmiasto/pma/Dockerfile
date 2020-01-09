FROM phpmyadmin/phpmyadmin:4.8.4

LABEL maintainer="j.roczniewski@trojmiasto.pl"

ADD Header.php /tmp/Header.php
ADD NavigationHeader.php /tmp/NavigationHeader.php

ADD run.sh /run.sh

ENTRYPOINT [ "/run.sh" ]
CMD ["supervisord", "-n", "-j", "/supervisord.pid"]
