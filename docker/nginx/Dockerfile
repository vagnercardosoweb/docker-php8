FROM nginx:1.25-alpine

ENV TZ=America/Sao_Paulo
RUN apk add --update --no-cache tzdata

# RUN usermod -u 1000 nginx

COPY ./nginx.conf /etc/nginx/conf.d/default.conf
