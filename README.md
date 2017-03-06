# DigitalOcean Ubuntu server with Postgres and connecting with Postico

**Installation**

Ubuntu's default repositories contain Postgres packages, so we can install these easily using the apt packaging system.

Since this is our first time using apt in this session, we need to refresh our local package index. We can then install the Postgres package and a -contrib package that adds some additional utilities and functionality:

`sudo apt-get update`
`sudo apt-get install postgresql postgresql-contrib`

**Managing DB users**

You can now access the postgres default account and run PostgreSQL prompts by typing

`sudo -u postgres psql`

you can end the Postgres prompt session by typing `\q`

By default, the postgres user has no DB password set on Ubuntu. This means that you can login to that account only by using the posgres OS user account.

If you want to access it from elsewhere(like Postico), then you need to set a password for postgres DB user:

Inside psql shell:

`ALTER USER postgres PASSWORD 'newPassword';`
(recommend `postgres` for password) 

(note - the semicolon is important)

[this shouldn't be necessary, but...]
If any commands are failing with an error psql: FATAL: password authentication failed for user "postgres" then check the file /etc/postgresql/8.4/main/pg_hba.conf: There must be a line like this as the first non-comment line:

`local   all         postgres                          ident`

**Creating a New Database**

From the linux shell:

`sudo -u postgres createdb 'dbName'`

**Connecting with Postico**

These instructions assume that you're set up to connect with SSH.

From Postico homescreen, click 'New Favorite'

Give your connection a Nickname that pleases you.

Host: `localhost`
The default port should work: `5432`
User: `postgres`
Password: recommend `posgres`

/////////

Database: `dbName` that you set above
SSH host: This will be the IP address for your DigitalOcean droplet
User: `root` unless you've set up a different user in Ubuntu
Password: leave blank, since we're setting up to connect with SSH
From the `options` dropdown, choose `connect via SSH`
A new `private key` field will appear in your window. Here you choose the ssh key you've previously created. It should be `~/.ssh/id_rsa`

And click connect!



