# tpyc_c_db
Data for use with tpyc_c

The Actian Ingres DBMS needs to be installed and running on a machine we will refer to as the "Ingres host". The Actian Ingres client
tools need to be installed on a machine we will refer to as the "Ingres client". The host and the client can be the same machine; there 
is no requirementment that they be separate.

If the Ingres client is a separate machine you should define a vnode to reference the DBMS on the Ingres host. When you create a vnode
you give it a name. The following assumes that if you are using a vnode it will be called *myvnode*.

Clone this repository to the Ingres client machine.
```
git clone https:/github.com/quelgeek/tpyc_c_db.git tpyc_c_db
```

On the Ingres host, create a database with whatever name you prefer
(for example *tpyccdb*).
```
createdb tpyccdb
```
If the the host and client are one and the same, load the data.
```
cd tpyc_c_db
sql tpyccdb < copy.in > copy.in.log
```
If the client is a different machine use the vnode to load the data.
```
cd tpyc_c_db
sql myvnode::tpyccdb < copy.in > copy.in.log
```
# Note
After successfully loading the database and before using it, take a checkpoint so that it can quickly be restored to its initial state after a test run.
(There is no need to enable journaling unless the test is actually intended to determine the impact of journaling.) Run the checkpoint on the Ingres host.
```
ckpdb -l tpyccdb
```
