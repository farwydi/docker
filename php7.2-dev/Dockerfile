FROM ubuntu:latest

RUN sed -i 's/http:\/\/archive.ubuntu.com\/ubuntu\//http:\/\/mirror.yandex.ru\/ubuntu\//g' /etc/apt/sources.list

RUN apt-get update

RUN echo 'tzdata tzdata/Areas select Europe' | debconf-set-selections
RUN echo 'tzdata tzdata/Zones/Europe select Moscow' | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive apt-get install php -y

RUN apt-get install composer -y
RUN apt-get install php-curl -y
RUN apt-get install php-zip -y
RUN apt-get install php-mbstring -y
RUN apt-get install php-dom -y
RUN apt-get install php-xdebug -y
RUN apt-get install php-memcached -y

RUN apt-get install curl
RUN curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | bash
RUN apt-get update && apt-get install php7.2-phalcon

RUN apt-get install sudo -y
RUN apt-get install git -y

RUN git clone https://github.com/phalcon/phalcon-devtools.git
RUN ln -s /phalcon-devtools/phalcon.php /usr/bin/phalcon
RUN chmod ugo+x /usr/bin/phalcon

RUN adduser --ingroup root --disabled-password --gecos '' farwydi
RUN usermod -aG sudo farwydi

ADD sudoers.txt /etc/sudoers
RUN chmod 440 /etc/sudoers
RUN visudo -c

USER farwydi
WORKDIR /home/farwydi