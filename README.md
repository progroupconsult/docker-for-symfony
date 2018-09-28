# Docker stack for Symfony 3

## Installation

1. Install `docker`, `docker-compose`, `docker-sync`

2. Create a `.env` from the `.env.dist` file and adapt it according to the needs of the application

    ```sh
    $ cp .env.dist .env && vim .env
    ```
3. Build/run containers in detached mode and run docker-sync

    ```sh
    $ docker-compose build
    $ docker volume create --name=app-sync
    $ docker-compose up -d
    $ docker-sync start
    ```
    On the next run you may use `$ docker-sync-stack start` command which do `docker-compose up && docker-sync start`
    
    After rebuilding container or changing .yml file run `$ docker-sync clean`
    
4. Update your system's hosts file

5. Prepare the Symfony application
    1. Update Symfony parameters (*app/config/parameters.yml*)

    2. Composer install & create database

        ```sh
        $ docker-compose exec php bash
        $ composer install
        $ sf doctrine:database:create
        $ sf doctrine:schema:update --force
        $ sf server:start 0.0.0.0:8000
        ```

6. Yarn
    ```sh
        $ docker-compose run --rm nodejs yarn install
        $ docker-compose run --rm nodejs yarn run [command]
    ```
    to run command in watch mode use ```--watch```
    ```sh
        $ docker-compose run --rm nodejs yarn run [command] --watch
    ```
