FROM nginx:1.25-alpine

ENV TZ=${TZ:-UTC}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apk add --update --no-cache tzdata
# RUN usermod -u 1000 nginx

COPY ./default.conf /etc/nginx/conf.d/default.conf
