railspg [-h] [-c] [-u] [-e] new <project_name>

This program generates a basic rails project where all generated databases (development, test and production) are
postgres. The outcome is otherwise equivalent to the default 'rails new <project_name>'

      -h: get help
      -c: Create databases. If (1) postgres username and unix/Ubuntu username are identical
          (2) An env variable is set to posgres password, databases may be created.
          By default, the env variable name is PGRAILS_DATABASE_PASSWORD.-
          If the databases are NOT created, run 'rake db:create:all' after program execution.
      -u: change username. The default username is the current unix/Ubuntu username
      -e: set postgres password environment variable name. Useful if the env variable name is other than default

    REQUIREMENTS
       (1) Set up a postgres user with the same name as the current unix/Ununtu login name
               sudo -u postgres createuser -s <unix_ubuntu_username>
               sudo -u postgres psql
               \\password <unix_ubuntu_username>
       (2) Set env variable. You may need to execute the following prior to running the program.-
              PGRAILS_DATABASE_PASSWORD='my_postgres_password'
              export PGRAILS_DATABASE_PASSWORD'
          Or, include the following line in your .bashrc file
              export PGRAILS_DATABASE_PASSWORD='my_postgres_password'

    EXAMPLE USAGE
      railspg new <project_name>
      ralspg -c new <project_name>-
      railspg -cu <username> -e PG_PASSWORD new <project name>
