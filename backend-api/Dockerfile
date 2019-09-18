FROM golang:1.13.0

ENV GOPATH=""

USER root
# SQLite
RUN apt-get update && apt-get install sqlite3 libsqlite3-dev -y

WORKDIR /go
ADD . /go

RUN sqlite3 ./db/articles.sqlite3 < ./db/init.sql

RUN rm ./go.mod
RUN go mod init backend

CMD ["go", "run", "main.go"]