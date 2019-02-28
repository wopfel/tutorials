# Nextcloud with docker-compose

1. `mkdir nextcloud-docker`

2. `cd nextcloud-docker`

3. Place two files there:

- docker-compose.yml
- nginx.conf

4. `docker-compose up -d`

5. Open webbrowser: http://localhost:8080/

6. Set credentials for admin (username/password)

7. You're signed in now

8. Place a file in the docker volume, for example

```
vim /var/lib/docker/volumes/nextcloud-docker_nextcloud/_data/data/admin/files/Testdatei.txt
```

9. Observation: File is not visible on the Nextcloud web page

10. Exec into the nextcloud-docker_app_1 container (you could also use portainer)

```
docker-compose exec app bash
```

11. Rescan files by executing

```
su - www-data --shell /bin/bash
php /var/www/html/occ files:scan --path="/admin/files/"
logout
exit
```

Or, all in one command:

    docker-compose exec app /bin/su - www-data --shell /bin/bash --command 'php /var/www/html/occ files:scan --path="/admin/files/"'

12. The file can be seen on the web page now.

