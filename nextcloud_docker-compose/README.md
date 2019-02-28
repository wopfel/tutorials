Nextcloud with docker-compose

Create directory nextcloud-docker

cd into directory

Place two files there:
- docker-compose.yml
- nginx.conf

docker-compose up -d

Open webbrowser: http://localhost:8080/

Set credentials for admin (username/password)

You're signed in

Place a file in the docker volume, for example
vim /var/lib/docker/volumes/nextcloud-docker_nextcloud/_data/data/admin/files/Testdatei.txt

File is not visible on the Nextcloud web page

Exec into the nextcloud-docker_app_1 container (maybe using portainer)

Exec
- su - www-data --shell /bin/bash
- cd /var/www/html
- php ./occ files:scan --path="/admin/files/"

The file can be seen on the web page now.

