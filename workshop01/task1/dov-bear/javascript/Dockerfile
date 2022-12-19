FROM node:16

LABEL "name"="myapp"

ARG APP_DIR=/APP_DIR

RUN mkdir $APP_DIR

WORKDIR $APP_DIR

ADD main.js .
ADD package.json .
ADD package-lock.json .
ADD public public
ADD views views

RUN npm ci

ENV PORT=5000 INSTANCE_NAME='' INSTANCE_HASH=''

HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl http://localhost:${PORT}/healthz || exit 1

EXPOSE $PORT

ENTRYPOINT node main.js