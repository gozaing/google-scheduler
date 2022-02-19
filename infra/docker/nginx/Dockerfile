FROM node:14.2-alpine as node
FROM nginx:1.18-alpine
LABEL maintainer="gozaing"
SHELL ["/bin/ash", "-oeux", "pipefail", "-c"]

ENV TZ=UTC

RUN apk update && \
    apk add --update --no-cache --virtual=.build-dependencies g++

# node
COPY --from=node /usr/local/bin /usr/local/bin
# npm
COPY --from=node /usr/local/lib /usr/local/lib
# yarn
COPY --from=node /opt /opt
# nginx config file
COPY ./infra/docker/nginx/*.conf /etc/nginx/conf.d/

WORKDIR /work/backend