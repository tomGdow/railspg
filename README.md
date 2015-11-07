##railspg
railspg [-h] [-c] [-u] [-e] new project-name

This Bash program generates a basic rails project where all generated databases (development, test and production) are
postgres. The outcome is otherwise equivalent to the default 'rails new project-name'

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
               \password <unix_ubuntu_username>
       (2) Set env variable. You may need to execute the following prior to running the program.-
              PGRAILS_DATABASE_PASSWORD='my_postgres_password'
              export PGRAILS_DATABASE_PASSWORD'
          Or, include the following line in your .bashrc file
              export PGRAILS_DATABASE_PASSWORD='my_postgres_password'

    EXAMPLE USAGE
      railspg new <project_name>
      ralspg -c new <project_name>-
      railspg -cu <username> -e PG_PASSWORD new <project name>

## rootrails
  rootrails [-h] model-name || table-name [search-string]

This program sets the application root in a Ruby-on-Rails 'config/routes.rb' file.

    The first compulsory argument is the table or model name. If the Model name is
    given, it will be converted to lowercase and pluralized. <table_name> format is
    to be preferred.

    The second argument is the search string, which defaults to 'welcome#index'

    You will be given a chance to revise the input before any changes are made

      -h: get help

    REQUIREMENTS
       Execute from the root directory of the rails app

    EXAMPLE USAGE
      rootrails Product
      rootrails products
      rootrails commodities 'products#index'

    NOTE
       Pluralization is not very clever. An 's' is added to a word that does not
       end in 's'.  'Product' is converted to 'products'

##scaffoldp
 scaffoldp [-h]

This program executes the following commands:

       rails generate scaffold Product name:string description:text price:float
       rake db:migrate

      -h: get help

    REQUIREMENTS
       execute from the root directory of the rails app

##socatrails
socatrails [-h] [-c] [-s] [-p] [-l] <server-address>

This program enables public access to a Rails application running in development mode on localhost.-
An ssh tunnel is created that binds a remote server TCP port (default: 8088) to a local TCP port (default: 3000).-
A public port is exposed on the remote server (default: 8090) that routes traffic to the remote port bound to localhost.-

If the remote address is reachable at 'mysite.com', a Rails app running on locahost:3000 is publicly visible at 'mysite.com:8090'

      -h: get help
      -c: Execute code pertaining to the local machine. The command executed will be of the following form
          ssh -R <remote_port_number>:localhost:<rails_port_number>  <server_address> -N:
      -s: execute code pertaining to remote server. The command executed will be of the following form
          socat TCP-LISTEN:<listen_port_number>,fork,reuseaddr TCP-CONNECT:127.0.0.1:<remote_port_number> &
      -p: remote port number (default 8088)
      -r: rails port number (default: 3000)
      -l: listening port (default: 8090)

    REQUIREMENTS
      (1) socat must be installed on both machines
      (2) A Ruby-on-Rails app running locally

    DEFAULTS
      (1)  The default server address is tomgdow@tomgdow.com (tomgdow@46.101.11.172)  You will need your own server address.
      (2)  Code pertaining to the local machine is executed by default. There is no need to include the '-c' option
           To execute code pertaining to the remote server, include the '-s' option

    EXAMPLE USAGE
      (1)  (local) socatrails
           (remote server) socatrails -s

      (2)  (local) socatrails -p 8000
           (remote server) socatrails -s -p 8000 -l 8080

      (3)  (local) socatrails -p 8000  user@ip_addresss
           (remote server) socatrails -s -p 8000 -l 8080

    SPECIFIC EXAMPLE
           (local)  rails s -p 4000
           (local)  socatrails -r 4000  user@mysite.com
           (remote server)  socatrails -s -l 8090
           (browser) mysite.com:8090

    REFERENCE
        You, Juan (2013) Enabling Public Access To Development Machine (Developer Diary of Joon You) [Internet]
        Available at: https://www.selfthis.com/2013/05/03/enabling-public-access-to-development-machine/
