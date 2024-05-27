FROM node:lts-alpine3.18
RUN apk add --no-cache git openssh-client
WORKDIR /app
COPY package.json /app
RUN npm install 
RUN chown -R node.node /app/node_modules 
