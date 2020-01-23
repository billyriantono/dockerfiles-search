#reutilización de imagen ya existente en Docker Hub
FROM node

WORKDIR /mybalance

ADD . /mybalance

#puerto en uso
EXPOSE 3000

#comando que se ejecuta para que la api funcione
CMD ["npm", "start"]
