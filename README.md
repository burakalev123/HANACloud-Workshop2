# SAP HANA Cloud HDI Workshop

A small learning project demonstrating SAP HANA Cloud development with an HDI container and database artifacts deployed through an MTA project.

## What this repository contains

- `mta.yaml` — defines the database module and SAP HANA HDI container resource
- `db/` — database deployment module using `@sap/hdi-deploy`
- `db/src/.hdiconfig` — maps HDI artifact types to their deployer plugins
- `db/src/HDBMIGRATIONTABLES/` — example table definition managed with an `.hdbmigrationtable` artifact
- `db/src/HDBROLES/` — example HDI roles for read and data-load privileges

## Example database object

The workshop creates a sample transaction-style table named `TLOG_F_C` containing customer, order and product attributes. The model is intentionally simple and is used to demonstrate HDI deployment concepts rather than represent a production data model.

## Security examples

The repository includes examples of HDI roles with different privilege levels:

- `SELECT_ON_TLOG_F_C` — read-only access
- `LOAD_TLOG_F_C` — SELECT, INSERT, UPDATE and DELETE privileges
- `SELECT_ON_TLOG_F_C_WITH_GRANT#` — example role demonstrating grant-related access

## Project structure

```text
HANACloud-Workshop2/
├── mta.yaml
├── db/
│   ├── package.json
│   └── src/
│       ├── .hdiconfig
│       ├── HDBMIGRATIONTABLES/
│       │   └── TLOG_F_C.hdbmigrationtable
│       └── HDBROLES/
│           ├── LOAD_TLOG_F_C.hdbrole
│           ├── SELECT_ON_TLOG_F_C.hdbrole
│           └── SELECT_ON_TLOG_F_C_WITH_GRANT#.hdbrole
└── README.md
```

## Deployment concept

The root MTA descriptor defines a `db` module of type `hdb` and binds it to an `com.sap.xs.hdi-container` resource. The database module uses `@sap/hdi-deploy` to deploy the artifacts from `db/src` into that HDI container.

Typical SAP Business Application Studio / Cloud Foundry workflow:

```bash
npm install --prefix db
mbt build
cf deploy mta_archives/*.mtar
```

The exact commands and authentication steps depend on the SAP BTP / Cloud Foundry environment used for the workshop.

## Purpose

This repository is retained as a learning reference for SAP HANA Cloud topics such as:

- HDI containers
- MTA-based deployment
- `.hdbmigrationtable` artifacts
- HDI database roles and privileges
- `@sap/hdi-deploy`

It is a workshop repository, not a production application.
