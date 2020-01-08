###############################
## 4gekkman/docker-mysql-dev ##
###############################
## Оглавление
##  
##  1. Базовый образ и разработчики
##  2. Установить необходимые пакеты
##  3. Назначить cmd по умолчанию
##  4. Назначить entrypoint
##

# 1. Базовый образ и разработчики
FROM mysql:5.7.19
MAINTAINER German Manvelov <4gekkman@gmail.com>

# 2. Установить необходимые пакеты
RUN apt-get update && apt-get install -y \

  supervisor \
  ; exit 0

# 3. Назначить cmd по умолчанию
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor.d/supervisor-docker-mysql-dev.ini"]

# 4. Назначить entrypoint
# ENTRYPOINT ["docker-entrypoint.sh"]
