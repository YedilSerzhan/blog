---
title: "Pgperffarm_GSoC"
date: 2022-09-10
---
Live server address: [http://140.211.168.145/](http://140.211.168.145/){:target="_blank"}

Github repo for the Server: [https://github.com/PGPerfFarm/pgperffarm_server](https://github.com/PGPerfFarm/pgperffarm_server){:target="_blank"}
> contributing branch at the moment: [https://github.com/PGPerfFarm/pgperffarm_server/tree/django_template_with_new_models](https://github.com/PGPerfFarm/pgperffarm_server/tree/django_template_with_new_models){:target="_blank"}

Github repo for the client: [https://github.com/PGPerfFarm/pgperffarm](https://github.com/PGPerfFarm/pgperffarm){:target="_blank"}



# Pgperffarm - Google Summer of Code 2022

PostgreSQL is an excellent and progressively refined database management system. To test its performance, the Postgres Performance Farm (short for Pgperffarm) was born as a result of the efforts of GSOC developers in previous years. In order to improve Pgperffarm even more, this year the GSOC project was planned to be improved on the following aspects:

* Add new benchmarking types to the client. (like fair use derivations based on the TPC-H and YCSB benchmark)
* Refactor the front-end with Django templates.
* Add new features to the backend. (e.g. Adding email notification feature)
* Add custom query feature for Pgbench benchmark.


## Client
The Client was a Python script that clones the PostgreSQL source code from a specific branch and creates a temporary PostgreSQL cluster. Then runs pgbench and collect the results and finally uploads the results to the backend. 

The main change to the client is adding a Fair use derivation of TPC-H Benchmark, of which the code is stored in the folder `pgtpch`. The whole process consists of building the TPC-H tool dbgen, generting TPC-H data and queries depending on the scale factor, initializing different versions of Postgres cluster, initializing the database and creating the tables, loading the data to the table, and executing the queries (power and througput tests) according to the TPC-H standard and measure the performance.

Secondly the structure of the workflow in the `perffarm-client.py` is changed. Users can now select which benchmarks (Pgbench and TPC-H like) and which configurations they want to run the client with.

Thirdly the client supports custom database name and the upload function supports basic auth now. 

## Back-end

The backend was a REST-API service written in Django to work with the vanilla Javascript frontend to receive and supply benchmarking statistics.

In order to add new benchmarks, modifications to the database structure is done. Adding new models and changing the existing ones but also not violating 3NF the database design principle.

Secondly to incorporate with frontend changing to Django template, each backend view function needs to be changed from returning JSON data to returning Django template instead.

The email notification is also implemented on the server so that in case the performance drops, the user will be notified.

## Front-end

The front-end was a website written in vanilla Javascript. 

And this year the whole website is rewritten with Django template.

Webpages for the TPC-H part are also added. For the TPC-H trend and query result, charts and digrams are added with D3.js.

## Weekly Completed Tasks


### June 13 ~ June 27

- Rewrote part of the front with Django template. (from [f02992f](https://github.com/PGPerfFarm/pgperffarm_server/commit/f02992fc327fceccf9260999d587ac3f5eb973f1){:target="_blank"} to [7045be2](https://github.com/PGPerfFarm/pgperffarm_server/commit/7045be257345c223bdbf97cb800c4761913be511){:target="_blank"} )
- Added basic authentication option to the server and client. ([23316d2](https://github.com/PGPerfFarm/pgperffarm/commit/23316d242c51492ff38bf61db445d6385cd234ad){:target="_blank"})
- Deployed the project on the server. [http://140.211.168.145/](http://140.211.168.145/){:target="_blank"}

### June 27 -  July 11 

- Finished rewriting the front-end with Django template. (from [fe34e81](https://github.com/PGPerfFarm/pgperffarm_server/commit/fe34e811e6fe0039bfe44d57318b1cd8fabc7d8a){:target="_blank"} to [a4d4e07](https://github.com/PGPerfFarm/pgperffarm_server/commit/a4d4e07ad5af305c72993ea43b926e334a3d20ea){:target="_blank"} )

### July 11 - Aug 12  

- Added TPC-H benchmark to the back-end and front-end. (from [e34bf07](https://github.com/PGPerfFarm/pgperffarm_server/commit/e34bf078025babaf4c04ca3e0082ff559b611c62){:target="_blank"} to [70ee15d](https://github.com/PGPerfFarm/pgperffarm_server/commit/70ee15dfbb70b91f755e7fc97baa4f9f94bb0dd0){:target="_blank"})
- Added email notification feature to the back-end. (from [b608234](https://github.com/PGPerfFarm/pgperffarm_server/commit/b608234ab7c0d538b7eb2e32e500004810015207){:target="_blank"} to [f7298be](https://github.com/PGPerfFarm/pgperffarm_server/commit/f7298be31710e8550a17f462578b5a4a68884378){:target="_blank"})
- Unified chart packages to d3.js.  ([e8e27e5](https://github.com/PGPerfFarm/pgperffarm_server/commit/e8e27e5e9861ad403062014933f18c79a3f35062){:target="_blank"})

### Aug 19 - 26 

- Redesigned the database schema and applied changed to the back-end. ([a861887](https://github.com/PGPerfFarm/pgperffarm/commit/6d279f115c675975e4a1d1ef419908e85271079c){:target="_blank"})
- Updated client workflow.  ([cda152b](https://github.com/PGPerfFarm/pgperffarm/commit/cda152b9b50c3fcd484d0d58f1d195d1cacf3ea4){:target="_blank"})

### Aug 26 - Sep 9
- Integration test & debugging.
- Added support for custom database name. ([2993f26](https://github.com/PGPerfFarm/pgperffarm/commit/2993f2608c9dee9066982f569348454f991a5784){:target="_blank"})
- Finalized documentation. 
