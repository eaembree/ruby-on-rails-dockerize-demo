# README

The project is built attemptinng to follow along with the docker-compose quickstart instructions at https://docs.docker.com/compose/rails/

Differences from the quickstart:
*  The postgres image no longer allows no password to be used. In docker-compolse.yml the `POSTGRES_PASSWORD` environment variable must be set to establish what the password is for the default `'postgress'` super user (there is another environment variable used to set the desired user). In addition that same password will then have to be set in config/databse.yml. This repo currently has those values as static text but there are methods to load them from environment variables instead which may be show in future commits.

Important Notes:
*  It is important to note when running docker on Linux everything in docker will try to run as root. So often docker and docker-compose commands must be prefixed with `sudo`. Docker has instructions on its site for how to setup group permissions to get around this. I encountered this problem when the containers try to clean the tmp/db/* files.
*  `docker-compose up` will process the docker-compose.yml file and start the containers but the shell will remain attached to the docker process(es). `CTRL+C` to terminate.  Alternatively, `docker-compose up -d` will start the containers detatched from the shell. Run docker-compose down to stop the containers.
*  `docker-compose up` will automatically build missing images but won't look for any changes that might affect existing images.
  *  `docker-compose up --build` or `docker-compose build` can be used to rebuild images for simple changes in the compose file (Ex: top level change to an exposed port mapping)
  *  `docker-compose run web bundle install` will have to be used to rebuild everything if there are changes to the Gemfile
