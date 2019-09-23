FROM node:10.14.1 as build
COPY package.json package-lock.json /web/
WORKDIR /web
RUN npm ci
COPY src/ /web/src
COPY angular.json tsconfig.json tslint.json /web/
RUN npm run build-prod

FROM alpine:3.8

RUN apk add --update --no-cache \
    lighttpd \
    && rm -rf /var/cache/apk/*

RUN mkdir /var/www/web
COPY --from=build /web/dist/web /var/www/web

COPY lighttpd.conf /etc/lighttpd/lighttpd.conf

EXPOSE 80

ENTRYPOINT ["lighttpd", "-D", "-f", "/etc/lighttpd/lighttpd.conf"]
