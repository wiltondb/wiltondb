[WiltonDB](https://wiltondb.com/)
=================================

Modified [PostgreSQL](https://www.postgresql.org/) with [Babelfish extensions](https://babelfishpg.org/) packaged for Windows and Linux.

Link to [documentation](https://github.com/wiltondb/wiltondb/wiki).

News
----

**2025-01-21**

WiltonDB 3 LTS (version 13.18.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3-lts-13-18-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows).

This update includes a fix to the error when a procedure is called with an empty table-valued parameter ([#97](https://github.com/wiltondb/wiltondb/issues/97)).

**2024-11-19**

WiltonDB 3 LTS (version 13.17.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3-lts-13-17-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

Notable changes:

 - security patches and bugfixes from upstream [PostgreSQL 15.9](https://www.postgresql.org/about/news/postgresql-171-165-159-1414-1317-and-1221-released-2955/) and [15.10](https://github.com/postgres/postgres/commit/b57d9d2e5d5543cc0c4b2de70d65d7b7c4115da6)
 - fix to the problem with `time`, `datetime2` and `datetimeoffset` precision handling and the `bcp` utility ([#91](https://github.com/wiltondb/wiltondb/issues/91))

To upgrade the existing DB cluster run the following on Postgres connection:

```sql
ALTER EXTENSION "babelfishpg_common" UPDATE TO '3.3.6';
ALTER EXTENSION "babelfishpg_tsql" UPDATE TO '3.3.3';
```

**2024-11-03**

WiltonDB 3 LTS (version 12.16.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3-lts-12-16-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

**WARNING: THIS UPDATE IS NOT COMPATIBLE WITH DB CLUSTERS FROM PREIVIOUS WILTONDB VERSIONS**

This update includes breaking changes implemented to fix the [#2987](https://github.com/babelfish-for-postgresql/babelfish_extensions/issues/2987) problem. Because of this there is no update path from version `11.15.1` - new DB cluster must be created. On Windows this is done automatically - default installation directory is changed to `C:\Program Files\WiltonDB Software\wiltondb_3_lts`. On Linux the existing DB cluster needs to be removed before running `wiltondb-setup`. 

**2024-07-29**

WiltonDB 3.3 update (version 11.15.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-11-15-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

Bugfixes:

 - `CHECK CONSTRAINTS` hint support with bcp and related fixes ([#2628](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/2628))
 - query parameters of type `binary(8)` are no longer confused with `rowversion` type ([#24](https://github.com/wiltondb/wiltondb/issues/24))
 - resolve correct `INFORMATION_SCHEMA` views in T-SQL inline blocks ([#28](https://github.com/wiltondb/wiltondb/issues/28))

Windows build changes:

 - [Windows authentication](https://github.com/wiltondb/wiltondb/wiki/Windows-Authentication#setting-up-windows-authentication-in-wiltondb) support with SSPI ([#18](https://github.com/wiltondb/wiltondb/issues/18))
 - support adding backtraces to error messages in server log if debuginfo files available in `<install_dir>/symbols` directory. `wiltondb3.3_debug_11.15.1.msi` installer is provided that includes debuginfo files files. Note, running server with backtraces enabled may be up to 1.5 times slower than normal runs.

**2024-06-30**

WiltonDB 3.3 update (version 10.14.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-10-14-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

Microsoft Visual C++ Redistributable update:

Before installing this update on Windows **it is necessary to update [Microsoft Visual C++ Redistributable package](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to version `14.40.33810.0` or later**. Latest version of MSVC 2022 compiler has introduced incompatibility with older versions of Redistributable package (details: [1](https://developercommunity.visualstudio.com/t/Builds-against-MSVC-Redistributable-144/10690723), [2](https://developercommunity.visualstudio.com/t/Access-violation-in-_Thrd_yield-after-up/10664660#T-N10669053)), when running on older version of Redistributable package WiltonDB may randomly crash with the following message:

```
Faulting application name: postgres.exe, version: 15.0.4.24180, time stamp: 0x66803d50
Faulting module name: MSVCP140.dll, version: 14.36.32532.0, time stamp: 0x04a30cf0
Exception code: 0xc0000005
Fault offset: 0x0000000000012f58
Faulting application path: C:\Program Files\WiltonDB Software\wiltondb3.3\bin\postgres.exe
Faulting module path: C:\Windows\SYSTEM32\MSVCP140.dll
```

Bugfixes:

 - `OpenSSL` library is updated to version `3.0.14` that includes [one low-severity security fix](https://www.openssl.org/news/secadv/20240528.txt)
 - a number of fixes backported from upstream Babelfish. To apply the changes related to string literals handling in `COALESCE` function to existing DB clusters, it is necessary to upgrade `babelfishpg_common` extension to version `3.3.3` by running the following SQL on Postgres connection (default port `5432`):

```
ALTER EXTENSION "babelfishpg_common" UPDATE TO '3.3.3'
```

Notable changes:

 - this update introduces support for [jTDS JDBC driver](https://jtds.sourceforge.net/). Note, `useCursors` jTDS option is not supported - cursors are supported when used directly through JDBC API (excluding `cursor.last()` call)
 - `DEFAULT` keyword is supported as a parameter to T-SQL function and procedures.


**2024-05-16**

WiltonDB 3.3 update (version 8.13.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-8-13-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

Bugfixes:

 - this release includes a fix to [CVE-2024-4317](https://www.postgresql.org/support/security/CVE-2024-4317/) from upstream PostgreSQL 15.7. To apply the fix to existing DB clusters it is necessary to run `<installdir>/share/fix-CVE-2024-4317.sql` script on Postgres connection (default port `5432`)
 - [#2540](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/2540) fix is backported from upstream Babelfish. It fixes the problem when altering a table to add a column with `DEFAULT NEWID()` makes the values all the same value which is not the correct behaviour. To apply the fix to existing DB cluster it is necessary to run the following SQL on Postgres connection (default port `5432`):

```
ALTER EXTENSION "babelfishpg_common" UPDATE TO '3.3.2'
```

Notable changes:

 - support for `ALTER AUTHORIZATION ON DATABASE::<dbname> TO <login-name>` ([#1954](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/1954)) is backported from upstream Babelfish. It allows to easily create login-owned databases, see details on [Logins and users wiki page](https://github.com/wiltondb/wiltondb/wiki/Logins-and-users)
 - support for `FOR JSON AUTO` ([#2243](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/2243)) is backported from upstream Babelfish
 - default TDS debug logging, which was creating multiple log records for every connection, is disabled; this behaviour can be controlled by changing `babelfishpg_tds.tds_debug_log_level` system parameter from `0` (disabled) to `3` (max verbosity)

**2024-04-15**

WiltonDB 3.3 update (version 7.12.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-7-12-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

Changes:

 - a number of fixes in BCP import area ([#2422](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/2422), [#2455](https://github.com/babelfish-for-postgresql/babelfish_extensions/issues/2455), [#2462](https://github.com/babelfish-for-postgresql/babelfish_extensions/issues/2462), [#2468](https://github.com/babelfish-for-postgresql/babelfish_extensions/issues/2468), [#2486](https://github.com/babelfish-for-postgresql/babelfish_extensions/issues/2486))
 - [mimalloc](https://github.com/microsoft/mimalloc) allocator is added on Windows to improve ANTLR memory handling, this makes DB connection initialization 10-15% faster
 - [system_stats](https://github.com/EnterpriseDB/system_stats) extension is included with Windows installer and Linux packages, see details about its usage in [Database-monitoring](https://github.com/wiltondb/wiltondb/wiki/Database-monitoring)

**2024-03-29**

Initial version of [WiltonDB Data Transfer GUI tool](https://github.com/wiltondb/wiltondb/wiki/WiltonDB-Data-Transfer-GUI-tool) is [released](https://github.com/wiltondb/wdb_transfer/releases).

WiltonDB 3.3 update (version 6.11.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-6-11-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows). This update includes a Windows-only fix to intermittent problem with BCP imports ([#13](https://github.com/wiltondb/wiltondb/issues/13)).

**2024-03-17**

WiltonDB 3.3 update (version 5.10.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-5-10-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

This update includes two notable bugfixes from upstream Babelfish - [#1957](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/1957) and [#2017](https://github.com/babelfish-for-postgresql/babelfish_extensions/pull/2017). The former one introduces additional `CASTs` in `babelfishpg_common` extension, its version is bumped from `3.3.0` to `3.3.1`. When performing the upgrade from previous versions of WiltonDB 3.3 (using existing DB cluster), it is necessary to run the following SQL on Postgres connection (port `5432` by default):

```
ALTER EXTENSION "babelfishpg_common" UPDATE TO '3.3.1'
```

**2024-03-02**

WiltonDB 3.3 update (version 4.9.1) is [released](https://github.com/wiltondb/wiltondb/releases/tag/3.3-4-9-1) for [Windows](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-windows) and [Linux](https://github.com/wiltondb/wiltondb/wiki/Getting-Started#wiltondb-on-linux).

With this update [Linked Servers and OPENQUERY](https://github.com/wiltondb/wiltondb/wiki/Linked-Servers-and-OPENQUERY) functionality is now supported in Linux packages the same way it works on Windows (issue [#9](https://github.com/wiltondb/wiltondb/issues/9)).

This update includes bugfixes to issues [#10](https://github.com/wiltondb/wiltondb/issues/10) and [#11](https://github.com/wiltondb/wiltondb/issues/11). This requires minor changes to stored procedures and views in `babelfishpg_tsql` extension, its version is bumped from `3.3.0` to `3.3.1`. When performing the upgrade from previous versions of WiltonDB 3.3 (using existing DB cluster), it is necessary to run the following SQL on Postgres connection (port `5432` by default):

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
