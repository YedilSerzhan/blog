---
title: "Pgperffarm_GSOC"
date: 2022-09-10
---

Github repo for the Server: https://github.com/PGPerfFarm/pgperffarm_server
> contributing branch at the moment: https://github.com/PGPerfFarm/pgperffarm_server/tree/django_template_with_new_models

Github repo for the client: https://github.com/PGPerfFarm/pgperffarm
> contributing branch at the moment: https://github.com/PGPerfFarm/pgperffarm/tree/new_models_tpch


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

- Added basic authentication to the back-end and front-end.
- Deployed the project on the server.


### June 27 -  July 11 

- Rewrote the front-end with Django template

### July 11 - 25 

- Added TPC-H benchmark to the back-end and front-end.

### July 29 - Aug 12 

- Added email notification feature to the back-end.
- Unified chart packages to d3.js.

### Aug 19 - 26 

- Redesigned the database schema and applied changed to the back-end.
- Updated client workflow.

### Aug 26 - Sep 9
- Integration test & debugging.
- Added support for custom database name.
- Finalized documentation.
