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

