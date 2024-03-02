[WiltonDB](https://wiltondb.com/)
=================================

Modified [PostgreSQL](https://www.postgresql.org/) with [Babelfish extensions](https://babelfishpg.org/) packaged for Windows and Linux.

Link to [documentation](https://github.com/wiltondb/wiltondb/wiki).

News
----

**2024-03-02**

WiltonDB 3.3 update (version 4.9.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-4-9-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

With this update [Linked Servers and OPENQUERY](https://github.com/wiltondb/wiltondb/wiki/Linked-Servers-and-OPENQUERY) functionality is now supported in Linux packages the same way it works on Windows.

This updates includes bugfixes to issues #10 and #11. This requires minor changes to stored procedures and views in `babelfishpg_tsql` extension, its version is bumped from `3.3.0` to `3.3.1`. When performing the upgrade from previous versions of WiltonDB 3.3 (using existing DB cluster), it is necessary to run the following SQL on Postgres connection (port `5432` by default):

```
ALTER EXTENSION "babelfishpg_tsql" UPDATE TO '3.3.1'
```

**2024-02-23**

WiltonDB 3.3 update (version 4.7.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-4-7-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows).

This update includes support for [Linked Servers and OPENQUERY](https://github.com/wiltondb/wiltondb/wiki/Linked-Servers-and-OPENQUERY).

**2024-02-12**

WiltonDB 3.3 update (version 4.6.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-4-6-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

With this update plain ZIP bundle is provided for Windows that can be used to set up and run WiltonDB [under non-privileged user](https://github.com/wiltondb/wiltondb/wiki/Running-under-non%E2%80%90privileged-user).

This update includes a [security fix from PostgreSQL 15.6](https://www.postgresql.org/about/news/postgresql-162-156-1411-1314-and-1218-released-2807/) and a critical fix from `BABEL_3_3_STABLE` branch of the [upstream Babelfish](https://github.com/babelfish-for-postgresql/babelfish_extensions/commits/6cc9e2307f498c48993f37c48bf40f2e6195d407/).

**2024-01-17**

Initial version of WiltonDB Backup GUI tool is [released](https://github.com/wiltondb/wdb_backup/releases/tag/1.0.0). Description about it is [added to documentation](https://github.com/wiltondb/wiltondb/wiki/WiltonDB-Backup-GUI-tool) along with more broad [article about backup and restore](https://github.com/wiltondb/wiltondb/wiki/Backup-and-restore-overview-in-Babelfish).

**2023-12-31**

WiltonDB 3.3 update (version 3.5.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-3-5-1).

This update includes [security fixes from PostgreSQL 15.5](https://www.postgresql.org/about/news/postgresql-161-155-1410-1313-1217-and-1122-released-2749/) and critical fixes from `BABEL_3_3_STABLE` branch of the [upstream Babelfish](https://github.com/babelfish-for-postgresql/babelfish_extensions/commits/472b82c295135640b5ef4c3d195c57657aed25c2/).

The update is released for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux) including [Ubuntu 23.10](https://github.com/wiltondb/wiltondb/issues/2#issuecomment-1873028158) (in preparation for Ubuntu 24.04 LTS) and a stable version for [Fedora x86_64](https://github.com/wiltondb/wiltondb/issues/3#issuecomment-1872142517).

**2023-11-15**

WiltonDB is covered on [postgresql.org](https://www.postgresql.org/about/news/wiltondb-33-released-2750/).

**2023-11-05**

Initial version of WiltonDB 3.3 [is released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-2-4-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).


License information
-------------------

WiltonDB is released under the [Apache-2.0](https://www.apache.org/licenses/LICENSE-2.0) or [PostgreSQL](https://opensource.org/license/postgresql/) license at your choice. Use is permitted under either license.
