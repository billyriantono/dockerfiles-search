# Stage 1
FROM node:8 as react-build
LABEL maintainer="Roland Ihms roland@ihmsmedia.com>"


# Clone our private GitHub Repository
ARG CACHEBUST=22
RUN git clone -b master https://943088905e8ab81cff9f1a900b63a2a057086cf3:x-oauth-basic@github.com/rolandihms/wanderers.org.na.git /app/

ENV IA_BUS_ID=$IA_BUS_ID
ENV IA_API_URL=$IA_API_URL
ENV IA_BACKEND_URL=$IA_BACKEND_URL

WORKDIR /app
#COPY . ./
RUN yarn
RUN yarn build

# Running the app
CMD [ "yarn", "start" ]
# Stage 2 - the production environment
