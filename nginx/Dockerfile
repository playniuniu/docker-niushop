FROM nginx:alpine
LABEL maintainer="playniuniu@gmail.com"

COPY default.conf /etc/nginx/conf.d/default.conf

RUN mkdir -p /opt/web

WORKDIR /opt/web
EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
