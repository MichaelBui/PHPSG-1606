# PHP Development with Docker (June 2016)

* Speaker: Michael Bui <[mf.michaelbui@gmail.com](mf.michaelbui@gmail.com)>
* Slide: http://www.slideshare.net/MichaelBui4/php-development-with-docker-63633984
* Docker images: https://github.com/gigary/docker-images

## Requirements
* A PHP Application ready (for this demo, do not for get to run `composer install` from inside `src`)
* Docker (Available for Linux/Mac OSX/Windows)
* A PHP IDE that support xDebug (Highly recommend [PHPStorm](https://www.jetbrains.com/phpstorm/))

## Instruction
**NOTE**: You should be inside directory `PHPSG-2016` for your best experience to run commands

### Run:
* Run `docker-compose -f docker-compose.prod.yml -p phpsg-prod up -d`
* Open `http://localhost:8000`, you should see your production-ready website

### Debug
* Run `docker-compose -f docker-compose.dev.yml -p phpsg-dev up -d`
* Open `http://localhost:8800`, you should see your in-development website
* To debug:
    * For your PHP IDE
        * Turn on Debug mode in your PHP IDE
        * Set a breakpoint in your PHP code
    * For your browser
        * Install a xdebug extension helper for your browser
        * Configure the xdebug value to match your setting in your .ini file (`PHPSTORM` for this demo)
        * Enable xdebug helper on your browser
    * Refesh/open your dev page. You should see php processing paused at your breakpoint
* **NOTE:**
    * There are known issue with docker beta for mac/win to prevend PHP send debug request to your PHP IDE
    * The current workaround is adding an network alias to your host machine: `sudo ifconfig lo0 alias 10.254.254.254`. After that, set the `xdebug.remote_host` to `10.254.254.254`.

### Test
Run `docker-compose -f docker-compose.test.yml -p phpsg-test run phpunit`

You should be able to see your PHPUnit test results

*NOTE*: MySQL server take some time to be ready, you may see the error `SQLSTATE[HY000] [1049] Unknown database 'homestead'`
You just need to run the command again

### Deploy
This is vary from case to case so I will leave here some basic instructions:
* Build nginx docker image (with project data). See `Dockerfile.nginx`
* Build php docker image (with project data). See `Dockerfile.php`
* Push the images into [Docker Hub](https://hub.docker.com) using `docker push <repo-name>[:tag-name]`
* On production server(s) run the docker images (see `docker-composer.prod.yml` for reference - simply use the same file will not work)

## Exercise
* Get your hands dirty with this
* Understand about basic docker commands and how docker works
* There are known issues, please find it out and fix it. Don't forget to create a pull request (PR)

## Contribution
* This is just a sharing on my personal experience developing PHP application with Docker that may not optimal
* All contributions are welcome and highly appreciated

# Thank you!
