```erlang
Epgpb = poolboy + epgsql,
Desc   = "A standalone PostgreSQL database connection pool server 
       	    application, created to support declarative application 
	    composition".
```
--------------------------------------------------------------------

This code is not much more than the poolboy epgsql example with the
full epgsql API implementated in poolboy workers. A code generator
(see `gen/`) builds this application dynamically from the compiled
epgsql binaries.

## To use this with rebar:

 * declare epgpb as a dependency of your application, 
 * define your poolboy/epgsql configuration for the `epgpb` 
     application, 
 * run `rebar get-deps compile`, and
 * run erl and start the epgpb application.


## To build and run the example:

The example requires a dummy user and database. To allow the example
user to login, you need to modify your pg_hba.conf to include the
line:

```
local   db1     db1     password
```

To setup the example database and role (both "db1").

```bash
cd example
sudo -u postgres ./setup_run_as_user_postgres.sh
```

It will ask for a password for user db1, type in **abc123**. From there, it's just:

```
rebar get-deps compile
./start.sh
application:start(epgpb_example).
```
