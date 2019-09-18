FROM node:10.16.2-alpine

WORKDIR /app


RUN apk update && \
    npm install -g npm @vue/cli

ADD package.json /app
ADD package-lock.json /app

RUN npm install axios
RUN npm install
