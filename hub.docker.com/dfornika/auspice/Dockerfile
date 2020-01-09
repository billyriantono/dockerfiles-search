from node:current-slim
USER node
ENV NPM_CONFIG_PREFIX /home/node/.npm-global
ENV PATH $PATH:/home/node/.npm-global/bin
RUN npm install -g auspice@1.37.5
EXPOSE 4000
ENTRYPOINT ["auspice", "view"]
