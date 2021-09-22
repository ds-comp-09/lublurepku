FROM node:dubnium-alpine AS base
RUN apk -U add curl
WORKDIR /usr/src/app
EXPOSE 3000

FROM node:dubnium AS build
RUN npm install -g @angular/cli@~8.3.4

WORKDIR ./

# Install app dependencies
COPY package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY . ./app
RUN ng build

#API_URL
ARG CONTENT_API_URL=localhost
ENV CONTENT_API_URL="${CONTENT_API_URL}" 

FROM base as final
WORKDIR ./app
COPY --from=build ./app .
CMD [ "node", "app.js" ]
