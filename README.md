# TableTurn Website

## Requirements

Before calling any of the docker commands documented bellow, you _must_ declare the following variables in your `ENV`:

- `DB_NAME` is the name of the database to be created.
- `DB_PASSWORD` is the `root` database user password to use to connect.

On my computer, I like to use `zsh`'s dotenv plugin and have a `.env` such as:

```
DB_NAME=ttwebsite
DB_PASSWORD=S0methingRe4llySecret
```

This whay when I `cd` into the project folder, my `ENV` is properly populated.

## Infrastructure

The `docker-compose.yml` file defines the following services:

- The Joomla application itself as `app`.
- The MySQL database defined as `db`.

It also defines the following volumes:

- `app-html` mounted on the `app` container and will contain the CMS source code.
- `db-data` mounted on the `db` container and stores database data.

## Up and Running

- First, make sure you have a docker-swarm compatible `$DOCKER_HOST` configured (`docker swarm init` etc).
- Then simply deploy by running `docker stack deploy --compose-file docker-compose.yml ttwebsite`.
- You can verify the status of individual services by running `docker service ls` and look for `ttwebsite_` prefixed services.
- An overlay network should have been created, look in `docker network ls` for `ttwebsite_main`.
- You should be able to access `0.0.0.0:8080` and when asked for a database host simply input `db:3306` as the database container is visible from the app container.
