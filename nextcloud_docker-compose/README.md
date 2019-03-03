# Nextcloud with docker-compose

Following these steps you get a Nextcloud instance using docker-compose. 3 docker containers are running: a mariadb database, a nextcloud (fpm image), and an nginx proxy. The steps and config files are taken from the official [Nextcloud docker page on Github](https://github.com/nextcloud/docker), and slightly modified.

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

Hint: if you use this construct in an existing proxy with https, you may get an "access denied / csrf check failed" error when trying to connect with the Nextcloud iOS app. This post by Stefan Mayer-Popp (fuxx) on Github helped me: https://github.com/nextcloud/ios/issues/768#issuecomment-459670101. 

You have to enforce https by modifying the config.php file (/var/lib/docker/volumes/nextcloud-docker_nextcloud/_data/config/config.php):

```
  'overwrite.cli.url' => 'https://nextcloud.example.com',
  'overwriteprotocol' => 'https',
```

In my docker container, the url was set to http (overwrite.cli.url), and the overwriteprotocol line was missing. After changing the file and restarting the docker containers, I was able to log in in the iOS app.


