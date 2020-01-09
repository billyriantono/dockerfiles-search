FROM openresty/openresty:wheezy
RUN /usr/local/openresty/luajit/bin/luarocks install busted
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["sh"]