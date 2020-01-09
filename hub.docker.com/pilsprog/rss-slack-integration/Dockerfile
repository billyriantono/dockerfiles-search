FROM node:4.1.2-onbuild

MAINTAINER Snorre Magnus Davøen <snorremd@gmail.com>

RUN chmod +x /usr/src/app/entrypoint.sh

ENTRYPOINT ["/usr/src/app/entrypoint.sh"]

# Re-enable default command
CMD [ "npm", "start" ]
