# Taiga Turtle

Based on [ipedrazas/taiga-docker](https://github.com/ipedrazas/taiga-docker).

## Initialization

### Database

    docker run -it --link postgres:postgres --rm postgres sh -c "su postgres --command 'createuser -h "'$POSTGRES_PORT_5432_TCP_ADDR'" -p "'$POSTGRES_PORT_5432_TCP_PORT'" -d -r -s taiga'"

    docker run -it --link postgres:postgres --rm postgres sh -c "su postgres --command 'createdb -h "'$POSTGRES_PORT_5432_TCP_ADDR'" -p "'$POSTGRES_PORT_5432_TCP_PORT'" -O taiga taiga'";

If you want to access the database, run the following container:

    docker run -it --link postgres:postgres --rm postgres sh -c 'exec psql -h "$POSTGRES_PORT_5432_TCP_ADDR" -p "$POSTGRES_PORT_5432_TCP_PORT" -U postgres'

Once you are in psql you can check that indeed our user & database have been created:

    # To list the users defined in our system use the following command
    \du
    # To list the databases, the command is
    \list

### Backend

Before running our backend, we have to populate our database, to do so, Taiga provides a regenerate script that creates all the tables and even some testing data

    docker run -it --rm --link postgres:postgres ipedrazas/taiga-back bash regenerate.sh
