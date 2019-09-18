FROM golang:1.13.0-alpine as build

# USER root
# SQLite
# gcc libc-devがalpineに必要
RUN apk update \
    && apk add --no-cache sqlite git gcc libc-dev

WORKDIR /go/app
ADD . /go/app

COPY . .

RUN rm ./go.mod \
    && go mod init backend \
    # realizeを動かすのにgo getで2つ必要（必ずこの順番）
    && go get gopkg.in/urfave/cli.v2@master \
    && go get github.com/oxequa/realize

# article.sqlite3を生成して読み込み
RUN touch ./db/articles.sqlite3 && \
    sqlite3 ./db/articles.sqlite3 < ./db/init.sql

# バイナリファイルを生成しalpineにマルチステージビルド
RUN go build -o app

FROM alpine

WORKDIR /app

# buildイメージからコピー
COPY --from=build /go/app/app .

RUN addgroup go \
    && adduser -D -G go go \
    && chown -R go:go /app/app

CMD ["./app"]