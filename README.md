# odoo_develop

This project is a template to develop Odoo modules with Docker and PyCharm.

## Pre-requisites

Docker V2 or higher
PyCharm Professional

## Environment

Create a `.env` file with the following variables in the root of the project:

| Variable          | Description       | Default |
|-------------------|-------------------|---------|
| ODOO_PORT         | Odoo port         | 8069    |
| ODOO_PASSWORD     | Odoo password     | admin   |
| POSTGRES_PORT     | Postgres port     | 5432    |
| POSTGRES_PASSWORD | Postgres password | odoo    |
| POSTGRES_USER     | Postgres user     | odoo    |
| POSTGRES_DB       | Postgres database | develop |

## Configuration for PyCharm

### Docker

Go to `Preferences > Build, Execution, Deployment > Docker > Tools` and check `Use Compose V2`.

### Python interpreter

1. Go to `Preferences > Project: odoo_develop > Python Interpreter` and click on the gear icon.
2. Then click on `Add Interpreter` and select `On Docker Compose...`. In the `Service` field select `web` and click
   on `Next` two times.
3. In the `System Interpreter > Interpreter` field select `/usr/bin/python3` and click on `Create`.

### Project structure

1. Go to `Preferences > Project: odoo_develop > Project Structure` and click on the gear icon.
2. Select `addons`, `odoo` and `odoo-stubs` folders and click on `Sources`.

### Run/Debug configuration

#### First init the database

1. Go to `Run > Edit Configurations...` and click on the `+` icon.
2. Select `Python` and in the `Name` field write `First init`.
3. In the `Script path` select folder icon and select `odoo/odoo-bin` in the project directory.
4. In the `Parameters` field
   write `-c /etc/odoo/odoo.conf -i base -d $Prompt$ --stop-after-init`.
   > _When run, it will ask for the database name. Write name of the database and press enter._
5. In the `Python interpreter` field select `Project Default ...` and click on `OK`.

#### Update all Apps

1. Go to `Run > Edit Configurations...` and click on the `+` icon.
2. Select `Python` and in the `Name` field write `Update all Apps`.
3. In the `Script path` select folder icon and select `odoo/odoo-bin` in the project directory.
4. In the `Parameters` field
   write `-c /etc/odoo/odoo.conf -u all -d $Prompt$ --stop-after-init`.
   > _When run, it will ask for the database name. Write name of the database and press enter._
5. In the `Python interpreter` field select `Project Default ...` and click on `OK`.

#### Odoo run

1. Go to `Run > Edit Configurations...` and click on the `+` icon.
2. Select `Python` and in the `Name` field write `Odoo`.
3. In the `Script path` select folder icon and select `odoo/odoo-bin` in the project directory.
4. In the `Parameters` field
   write `-c /etc/odoo/odoo.conf`.
5. In the `Python interpreter` field select `Project Default ...` and click on `OK`.

### How to use Shell

 When you run the `Odoo` configuration, you can use the shell to run in terminal.

1. Go to `Services` tab and select `Docker-compose: <project name> > web > <project name>-web-1` service.
   > __NOTE:__ _The name of the service is the name of the project with `-web-1` at the end or similar._"
2. Right click and select `Create Terminal`.
3. In the terminal write `./odoo-bin shell -c /etc/odoo/odoo.conf -d <POSGTRES_DB>`.
   > __NOTE:__ _Replace `<POSGTRES_DB>` with the name of the database._
 
### Recommended Addons

* .env files support
* Rainbow CSV
* GitHub Copilot
* GutToolBox
* Odoo
* XPathView + XSLT