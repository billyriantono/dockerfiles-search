FROM yooqe/base


RUN aptitude update -y
RUN aptitude install -y memcached

EXPOSE 11211

ENTRYPOINT [ "/usr/bin/memcached" ]
CMD [ "-m", "128", "-p", "11211", "-u", "root" ]
