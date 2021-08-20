<p align="center">
    <img src="d4s.png" />
</p>


## Docker environment for [Jedisjeux](https://jedisjeux.net/) Project</h1>

For more information on how Jedisjeux works, please read all the [documentation](http://docs.jedisjeux.net)

## Installation

1. Clone docker4jedisjeux repository

    ```bash
    $ git clone git@github.com:Jedisjeux/Docker.git jedisjeux-docker
    ```

2. Clone Jedisjeux-Standard repository
    ```bash
    $ cd jedisjeux-docker
    $ git clone git@github.com:Jedisjeux/Jedisjeux.git jedisjeux
    ```

3. Run Docker's containers

   ```bash
   $ docker-compose up --build -d
   ```

4. Install Jedisjeux vendors

    ```bash
    $ docker-compose run --rm php composer install
    ```

5. Install Jedisjeux

    ```bash
    $ docker-compose run --rm php bin/console app:install
    ```

6. Install and build assets vendors

    ```bash
    $ docker-compose run --rm node yarn install
    ```
    ```bash
    $ docker-compose run --rm node yarn build
    ```

That's all. Try and fun!!!

This results in the following running containers:

```bash
$ docker-compose ps
         Name                        Command              State                      Ports
-------------------------------------------------------------------------------------------------------------
jedisjeux-docker_db_1        docker-entrypoint.sh mysqld      Exit 1                                             
jedisjeux-docker_elk_1       /usr/bin/supervisord -n -c ...   Up       0.0.0.0:81->80/tcp, 0.0.0.0:9201->9200/tcp
jedisjeux-docker_nginx_1     nginx -g daemon off;             Exit 1                                             
jedisjeux-docker_php_1       docker-php-entrypoint php-fpm    Up       9000/tcp                                  
jedisjeux-docker_php_run_9   docker-php-entrypoint bash       Up       9000/tcp                                  
jedisjeux-docker_traefik_1   /traefik --api --docker          Up       0.0.0.0:80->80/tcp, 0.0.0.0:8080->8080/tcp
-----------
```

## Testing

Inside the standard Jedisjeux modify the behat.yml.dist adding the following:

```yml
default:
    extensions:
        Behat\MinkExtension:
            base_url: "http://nginx"
            sessions:
                selenium2:
                    selenium2:
                        wd_host: http://selenium:4444/wd/hub
```
And run Behat:

```bash
    $ docker-compose run --rm php vendor/bin/behat
```
## License

This bundle is published under the [MIT License](LICENSE)

## Contributing

First of all, **thank you** for contributing ♥  
If you find any typo/misconfiguration/... please send me a PR or open an issue.  
Also, while creating your Pull Request on GitHub, please write a description which 
gives the context and/or explains why you are creating it.


http://159.69.2.71:81/

 email: loic_425@example.com
username: loic_425
password: admin
