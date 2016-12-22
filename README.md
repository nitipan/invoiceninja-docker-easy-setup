# invoiceninja-docker for localhost
This project simplifies the usage of [InvoiceNinja](https://github.com/invoiceninja/invoiceninja) leveraging [Docker](http://docker.com/) while maintaining a high level of security.

InvoiceNinja is a great tool for business owners to process invoices. However it's implemented as a webservice, which could expose clients' data to the Internet in case of security issues. Since security issues are not unlikely, this project avoids security problems by running InvoiceNinja only on localhost.

**Note that this is still beta quality and not for production use yet!**

Benefits of this setup
-----------
- InvoiceNinja will run only on localhost, and be accessible only from localhost.
- InvoiceNinja can be started and stopped when needed within milliseconds.
- InvoiceNinja will be able to send emails and invoices as long localhost is connected to the Internet.
- Backups are as easy as copying one folder.


Drawbacks
------------
- The client portal of InvoiceNinja will not work since it runs on localhost. In the portal, clients can see their invoices and download them. This is more secure than sending invoices via email, but a compromise of this setup.


How to setup
---------------
- Setup `docker` and `docker-compose` following Docker's official docs. Make sure you have `docker-compose` version >= 1.6. Also make sure you have `git` installed.
- Clone this repo to your machine:

  ```
  git clone git@github.com:MathiasRenner/invoiceninja-docker.git
  ```
- Change into the cloned directory with

  ```
  cd invoiceninja-docker
  ```

- When this has been finished download the necessary files and start InvoiceNinja with

  ```
  docker-compose up -d
  ```
  If everything was successful, the output of the previous command looks similar to this:

  ```
  Creating invoiceninjadocker_db_1
  Creating invoiceninjadocker_app_1
  Creating invoiceninjadocker_web_1
  ```

- Finally, open InvoiceNinja in Firefox at `http://localhost:8080/`. Congrats! Your local instance of InvoiceNinja is running! See the next section to see how to start and stop it.


How to start and stop it
--------------

### Start InvoiceNinja
- Make sure you are in the same repository where the `docker-compose.yml` resides and run

  ```
  docker-compose up -d
  ```

- Open InvoiceNinja in firefox at `http://localhost:8080/`

### Stop InvoiceNinja
- Make sure you are in the same repository where the `docker-compose.yml` resides and run

  ```
  docker-compose down
  ```

 **Note:** It's much faster if you use `unpause` and `pause` instead of `up -d` and `down`.


Backup & Restore
----------------
- Backup: All settings for InvoiceNinja are stored in the database, which resides in the folder `invoiceninja-docker/database`. If you copy this folder to a any different location, you have a backup.
- Restore: The only way to restore all settings is to restore the folder `database` – which is easy and fast. The backup/restore options inside InvoiceNinja don't cover all settings.


Troublehooting
-------------
- If you see a "Bad Gateway" in your browser instead of invoice ninja, wait some seconds and try again. If the error remains, a clean up with the following command probably resolves the problem: `docker rm -fv $(docker ps -aq)`.  *Note* that this command removes all containers and volumes on your machine!


TODOs
------------
- Automate start & stop with desktop icon for Ubuntu
