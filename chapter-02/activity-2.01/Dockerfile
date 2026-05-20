FROM ubuntu:22.04
LABEL maintainer=SS
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt install apache2 php libapache2-mod-php -y
COPY welcome.php /var/www/html
EXPOSE 80
ENTRYPOINT ["apache2ctl", "-D", "FOREGROUND"]
