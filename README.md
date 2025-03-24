# tpyc_c_db
Data for use with **tpyc_c.py**
> [!NOTE]
> In hindsight GitHub is not the best place to host this large and relatively static resource. It will probably be moved somewhere else in future. When that happens the new location will be noted here.

## Before You Start: Git Large File Storage
You will need to have installed [Git Large File Storage](https://git-lfs.com/) in order to clone this repository.

## Loading the tpyc_c Database
The Actian Ingres DBMS needs to be installed and running on a machine we will refer to as the "Ingres host". The Actian Ingres client
tools need to be installed on a machine we will refer to as the "Ingres client". The host and the client can be the same machine; there 
is no requirementment that they be separate.

Clone this repository to the Ingres client machine.
```
git clone https:/github.com/quelgeek/tpyc_c_db.git tpyc_c_db
```
The following data files are provided:
* **customer.data** 210MiB  
* **delivery.data** (empty) 
* **district.data** 16KiB 
* **history.data** 47MiB  
* **item.data** 11MiB     
* **new_order.data** 3.7MiB
* **order.data** 44MiB    
* **order_line.data** 558MiB
* **stock.data** 405MiB    
* **warehouse.data** 1.4KiB

On the Ingres host, create a database with whatever name you prefer
(for example **tpcc_db**).
```
createdb tpcc_db
```
If the the host and client are one and the same, load the data.
```
cd tpyc_c_db
sql tpcc_db < copy.in > copy.in.log
```
If the Ingres client is a separate machine you should define a vnode to reference the DBMS on the Ingres host. When you create a vnode
you give it a name (for example **myvnode**). To upload the data from the client to the a database called **tpcc_db** on the Ingres host:
```
cd tpyc_c_db
sql myvnode::tpcc_db < copy.in > copy.in.log
```
> [!TIP] 
> After successfully loading the database and _before_ using it, take a checkpoint so that it can quickly be restored to its initial state after a test run.
> (There is no need to enable journaling unless the test is actually intended to determine the impact of journaling.) Run the checkpoint logged in as the database
> owner on the Ingres host.
> ```
> ckpdb -l -w tpcc_db
> ```
