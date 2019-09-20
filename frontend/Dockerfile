FROM node:10.16.2-alpine

WORKDIR /app

RUN apk update && \
    npm install -Sg npm @vue/cli --no-optional

# npm installに必要なjsonファイルを用意
ADD package.json /app
ADD package-lock.json /app

RUN npm install axios -S --no-optional
RUN npm install --no-optional
