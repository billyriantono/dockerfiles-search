FROM base/archlinux

MAINTAINER Felipe Ruhland <felipe.ruhland@gmail.com>

RUN pacman -Sy --noconfirm postgresql-client 

CMD ["sh", "-c", "pg_dump -h $PGHOST -U $PGUSERNAME -w $PGDBNAME > /backup/dump_$(date -d 'today' +'%Y%m%d%H%M').sql"]
