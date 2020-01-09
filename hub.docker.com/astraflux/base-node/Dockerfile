# Build the docker container.
FROM node:4.0.0

# Metadata area.
MAINTAINER Martin Kreibe <mkreibe@astraflux.com>

# Define the environment.
ENV AFX_NODE_PORT=8080

ENV AFX_ROOT_PATH=/afx/frontend/
ENV AFX_PUBLIC_PATH=${AFX_ROOT_PATH}public/
ENV AFX_SOURCE_PATH=${AFX_ROOT_PATH}src/

# Add the volumes to the build.
WORKDIR ${AFX_SOURCE_PATH}

# Copy just the p
COPY /src/package.json ${AFX_SOURCE_PATH}

# Install all the dependancies.
RUN npm install

# Copy all the contents over.
COPY /public  ${AFX_PUBLIC_PATH}
COPY /src     ${AFX_SOURCE_PATH}

# Open the firewall.
EXPOSE ${AFX_NODE_PORT}

# Finally execute the script.
CMD ["node", "server.js"]