FROM ubuntu:22.04
RUN apt-get update && apt-get install apache2 -y
WORKDIR /var/www/html
COPY index.html .
CMD ["ls"]
