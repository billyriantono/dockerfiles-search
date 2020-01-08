FROM "spargo/web:latest"

# Copy build scripts
COPY --chown=root ./_scripts/ /

RUN chmod +x -R /spargo/build 

RUN /spargo/build/00-install_php.sh
