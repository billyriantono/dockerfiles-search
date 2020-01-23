# Imagen raíz
FROM node
# Carpeta raíz
WORKDIR /apitechu
# Copia de archivos
ADD . /apitechu

# Instalo los paquetes necesarios
RUN chgrp -R 0 /apitechu && \
    chmod -R g=u /apitechu

RUN npm install http-server -g

RUN npm install pm2 -g

RUN cd back && npm install
RUN cd gateway && npm install

EXPOSE 4000
EXPOSE 8082

#CMD ["pm2-runtime", "process.yml"]
CMD ["pm2-runtime", "--public", "grdlk3g97hoseuu", "--secret", "lo747nxigere093", "process.yml"]
