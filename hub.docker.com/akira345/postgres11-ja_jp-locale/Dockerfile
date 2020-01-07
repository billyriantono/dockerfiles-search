FROM postgres:11

# setting locale
RUN localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
ENV LANG ja_JP.utf8

# copy from custom postgresql.conf file
COPY ./postgresql.conf /etc/postgresql/postgresql.conf

# enable custom configuration
CMD ["-c", "config_file=/etc/postgresql/postgresql.conf"]
