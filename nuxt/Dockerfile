FROM node:13.10.1-alpine3.10

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

WORKDIR /app

RUN apk update && \
    apk upgrade && \
    npm install -g yarn && \
    apk add --no-cache \
    python \
    git

ENV HOST 0.0.0.0
EXPOSE 3333
