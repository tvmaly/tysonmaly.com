---
author: admintm
categories:
- postgresql
date: "2017-08-06T12:44:03Z"
guid: http://www.tysonmaly.com/?p=223
id: 223
title: how to backup and restore postgresql database
url: /postgresql/backup-restore-postgresql-database/
---

# How to backup and restore postgresql database 9.6

Having regular backups of your database is important as you might already know.   You might even have a development environment that you want to load with production data.   Here is quick overview of how you can backup your postgresql database and restore it.   This will also work if you are backing it up from Ubuntu linux and restoring it to Mac OSX.

Step 1. Run the pd_dump command, you will be prompted for a password in most cases, enter it when prompted:

<pre>pg_dump yourdatabasename  &gt; yourdatabase.20170806.sql</pre>

Step 2. Copy the file yourdatabase.20170806.sql to the computer you will restore it on

Step 3.  Run the psql command to restore using the file your created, you may be prompted for a password, enter if prompted

<pre>psql -d yourdatabase &lt; yourdatabase.20170806.sql</pre>

That is it, you should have a fully restored copy.

I also like to have a database creation script that sets up the database, a user, and two roles for that user that is used to grant privileges to.  One role will have less access to the database, and the other will have more.  This way you can revoke the role that has more access later one after you have finished your development.

If you have one of these scripts then you can get a really clean restore with no existing data.

Assume you have a file createdatabase.sql that creates database name, user, and roles you could first drop the database on your dev machine with the command:

dropdb &#8216;yourdatabase&#8217;

Then you could re-create it with

psql < createdatabase.sql

Then finally restore the database in full with:

<pre>psql -d yourdatabase &lt; yourdatabase.20170806.sql</pre>

Here is an example createdatabase.sql script, you should replace password with your password and yourdatabase with
  
your real database name:

<pre>CREATE DATABASE yourdatabase;

\connect yourdatabase;

CREATE SCHEMA version1;

CREATE ROLE dbuser LOGIN PASSWORD 'password' CREATEDB VALID UNTIL 'infinity';

CREATE ROLE dbadmin INHERIT;

CREATE ROLE dbrole INHERIT;

GRANT dbrole TO dbuser;

GRANT dbadmin TO dbuser;

GRANT USAGE ON SCHEMA version1 TO dbrole;

ALTER DEFAULT PRIVILEGES IN SCHEMA version1
GRANT SELECT, REFERENCES, TRIGGER ON TABLES
TO dbrole;

ALTER DEFAULT PRIVILEGES IN SCHEMA version1
GRANT SELECT, UPDATE ON SEQUENCES
TO dbrole;

ALTER DEFAULT PRIVILEGES IN SCHEMA version1
GRANT EXECUTE ON FUNCTIONS
TO dbrole;

ALTER DEFAULT PRIVILEGES IN SCHEMA version1
GRANT USAGE ON TYPES
TO dbrole;

GRANT ALL PRIVILEGES ON DATABASE "yourdatabase" TO dbadmin;

GRANT ALL PRIVILEGES ON SCHEMA version1 TO dbadmin;

GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA version1 TO dbadmin;

GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA version1 TO dbadmin;

GRANT ALL PRIVILEGES ON ALL FUNCTIONS IN SCHEMA version1 TO dbadmin;</pre>