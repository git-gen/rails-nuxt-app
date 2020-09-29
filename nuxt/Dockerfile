FROM node:14.11.0-alpine3.10

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

WORKDIR /app

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    python \
    make \
    g++ \
    git

COPY package.json /app/package.json

RUN yarn
RUN yarn build

ENV HOST 0.0.0.0
EXPOSE 3333

CMD [ "yarn", "start" ]
