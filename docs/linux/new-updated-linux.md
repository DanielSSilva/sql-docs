---
title: Updated - SQL Server on Linux docs | Microsoft Docs
description: Display snippets of updated content for recently changed in documentation, for Microsoft SQL Server on Linux.
services: na
documentationcenter: ''
author: MightyPen
manager: jhubbard
editor: rothja
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: linux-sql
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: updart-autogen
ms.date: 09/11/2017
ms.author: genemi
---
# New and Recently Updated: SQL Server on Linux docs



Nearly every day Microsoft updates some of its existing articles on its [Docs.Microsoft.com](http://docs.microsoft.com/) documentation website. This article displays excerpts from recently updated articles. Links to new articles might also be listed.

This article is generated by a program that is rerun periodically. Occasionally an excerpt can appear with imperfect formatting, or as markdown from the source article. Images are never displayed here.

Recent updates are reported for the following date range and subject:



- *Date range of updates:* &nbsp; **2017-07-18** &nbsp; -to- &nbsp; **2017-09-11**
- *Subject area:* &nbsp; **Microsoft SQL Server on Linux**.




&nbsp;

## New Articles Created Recently

The following links jump to new articles that have been added recently.


1. [DB Mail and Email Alerts with SQL Agent on Linux](sql-server-linux-db-mail-sql-agent.md)



&nbsp;

## Updated Articles with Excerpts

This section displays the excerpts of updates gathered from articles that have recently experienced a large update.

The excerpts displayed here appear separated from their proper semantic context. Also, sometimes an excerpt is separated from important markdown syntax that surrounds it in the actual article. Therefore these excerpts are for general guidance only. The excerpts only enable you to know whether your interests warrant taking the time to click and visit the actual article.

For these and other reasons, do not copy code from these excerpts, and do not take as exact truth any text excerpt. Instead, visit the actual article.





&nbsp;

<a name="compactupdatedlist"/>

## Compact List of Articles Updated Recently

This compact list provides links to all the updated articles that are listed in the Excerpts section.

1. [Operate HA availability group for SQL Server on Linux](#TitleNum_1)
2. [Configure SQL Server 2017 container images on Docker](#TitleNum_2)
3. [Configure SQL Server on Linux with the mssql-conf tool](#TitleNum_3)
4. [Customer Feedback for SQL Server on Linux](#TitleNum_4)
5. [Migrate a SQL Server database from Windows to Linux using backup and restore](#TitleNum_5)
6. [Release notes for SQL Server 2017 on Linux](#TitleNum_6)
7. [Installation guidance for SQL Server on Linux](#TitleNum_7)
8. [Install SQL Server Integration Services (SSIS) on Linux](#TitleNum_8)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### 1. &nbsp; [Operate HA availability group for SQL Server on Linux](sql-server-linux-availability-group-failover-ha.md)

*Updated: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 167.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1bef3ece125721b041aa2b9d836329736377df8d 669d2b9a614d680b98280d5b522ba82cf466536c  (PR=2948  ,  Filename=sql-server-linux-availability-group-failover-ha.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



**Upgrade availability group**


Before you upgrade an availability group, review the best practices at [Upgrading availability group replica instances--../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

The following sections explain how to perform a rolling upgrade with SQL Server instances on Linux with availability groups.

**Upgrade steps on Linux**


When availability group replicas are on instances of SQL Server in Linux, the cluster type of the availability group is either `EXTERNAL` or `NONE`. An availability group that is managed by a cluster manager besides Windows Server Failover Cluster (WSFC) is `EXTERNAL`. Pacemaker with Corosync is an example of an external cluster manager. An availability group with no cluster manager has cluster type `NONE` The upgrade steps outlined here are specific for availability groups of cluster type `EXTERNAL` or `NONE`.

1. Before you begin, backup each database.
2. Upgrade instances of SQL Server that host secondary replicas.

    a. Upgrade asynchronous secondary replicas first.

    b. Upgrade synchronous secondary replicas.

   >[!NOTE]
   >If an availability group only has asynchronous replicas - to avoid any data loss change one replica to synchronous and wait until it is synchronized. Then upgrade this replica.

   b.1. Stop the resource on the node hosting the secondary replica targeted for upgrade

   Before running the upgrade command, stop the resource so the cluster will not monitor it and fail it unnecessarily. The following example adds a location constraint on the node that will result on the resource to be stopped. Update `ag_cluster-master` with the resource name and `nodeName1` with the node hosting the replica targeted for upgrade.

```
   pcs constraint location ag_cluster-master avoids nodeName1
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### 2. &nbsp; [Configure SQL Server 2017 container images on Docker](sql-server-linux-configure-docker.md)

*Updated: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 257.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0239ed55a23721eedcc0407a0886d08da47c975b 108fe230151cff7dc91fcdc22218f232394746ec  (PR=3050  ,  Filename=sql-server-linux-configure-docker.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=60272ce672c0a32738b0084ea86f8907ec7fc0a5) -->



1. Identify the Docker **tag** for the release you want to use. To view the available tags, see [the mssql-server-linux Docker hub page](https://hub.docker.com/r/microsoft/mssql-server-linux/tags/).

1. Pull the SQL Server container image with the tag. For example, to pull the RC1 image, replace `<image_tag>` in the following command with `rc1`.

```
   docker pull microsoft/mssql-server-linux:<image_tag>
```

1. To run a new container with that image, specify the tag name in the `docker run` command. In the following command, replace `<image_tag>` with the version you want to run.

```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1401:1433 -d microsoft/mssql-server-linux:<image_tag>
```

These steps can also be used to downgrade an existing container. For example, you might want to rollback or downgrade a running container for troubleshooting or testing. To downgrade a running container, you must be using a persistence technique for the data folder. Follow the same steps outlined in the [upgrade section--#upgrade), but specify the tag name of the older version when you run the new container.

> [!IMPORTANT]



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### 3. &nbsp; [Configure SQL Server on Linux with the mssql-conf tool](sql-server-linux-configure-mssql-conf.md)

*Updated: 2017-09-05* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2) | [Next](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= lbosq.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6117f03e9617b70077488d86f94b32537c4cb9e8 4247a749c056037dd71a27121525be04be6a4f21  (PR=3042  ,  Filename=sql-server-linux-configure-mssql-conf.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=46b16dcf147dbd863eec0330e87511b4ced6c4ce) -->



**<a id="localaudit"></a> Set local audit directory**


The **telemetry.userrequestedlocalauditdirectory** setting enables Local Audit and lets you set the directory where the Local Audit logs are created.

1. Create a target directory for new Local Audit logs. The following example creates a new **/tmp/audit** directory:

```
   sudo mkdir /tmp/audit
```

1. Change the owner and group of the directory to the **mssql** user:

```
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
```

1. Run the mssql-conf script as root with the **set** command for **telemetry.userrequestedlocalauditdirectory**:

```
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
```

1. Restart the SQL Server service:

```
   sudo systemctl restart mssql-server
```

For more information, see [Customer Feedback for SQL Server on Linux--sql-server-linux-customer-feedback.md).

**<a id="lcid"></a> Change the SQL Server locale**


The **language.lcid** setting changes the SQL Server locale to any supported language identifier (LCID).

1. The following example changes the locale to French (1036):

```
   sudo /opt/mssql/bin/mssql-conf set language.lcid 1036
```

1. Restart the SQL Server service to apply the changes:

```
   sudo systemctl restart mssql-server
```

**<a id="memorylimit"></a> Set the memory limit**


The **memory.memorylimitmb** setting controls the amount physical memory (in MB) available to SQL Server. The default is 80% of the physical memory.

1. Run the mssql-conf script as root with the **set** command for **memory.memorylimitmb**. The following example changes the memory available to SQL Server to 3.25 GB (3328 MB).

```
   sudo /opt/mssql/bin/mssql-conf set memory.memorylimitmb 3328
```

1. Restart the SQL Server service to apply the changes:



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### 4. &nbsp; [Customer Feedback for SQL Server on Linux](sql-server-linux-customer-feedback.md)

*Updated: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_3) | [Next](#TitleNum_5))

<!-- Source markdown line 104.  ms.author= anshrest.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9d8122e864804004d91f6b7c5c3d24c4a4114d34 7316ef831c390a854c324f23a02c3fb6005e2fea  (PR=2948  ,  Filename=sql-server-linux-customer-feedback.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->




**On Docker**

To enable Local Audit on docker you must have Docker [persist your data--sql-server-linux-configure-docker.md).

1. The target directory for new Local Audit logs will be in the container. Create a target directory for new Local Audit logs in the host directory on your machine. The following example creates a new **/audit** directory:

```
   sudo mkdir <host directory>/audit
```


1. Add an `mssql.conf` file with the lines `[telemetry]` and `userrequestedlocalauditdirectory = <host directory>/audit` in the host directory:

```
   echo '[telemetry]' >> <host directory>/mssql.conf
```

```
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
```
2. Run the container image
```
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

```
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" --cap-add SYS_PTRACE -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux
```

**Next steps**





&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### 5. &nbsp; [Migrate a SQL Server database from Windows to Linux using backup and restore](sql-server-linux-migrate-restore-database.md)

*Updated: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_4) | [Next](#TitleNum_6))

<!-- Source markdown line 30.  ms.author= mikeray.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e78f5516a46eab834f644979d3e1c0ca415fabcd 6b03a01385078290b9f451ac013b628f53e0e8b4  (PR=2948  ,  Filename=sql-server-linux-migrate-restore-database.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



* Windows machine with the following:
  * [SQL Server](https://www.microsoft.com/sql-server/sql-server-2016-editions) installed.
  * [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) installed.
  * Target database to migrate.

* Linux machine with the following installed:
  * SQL Server 2017 RC2. See the installation quickstarts for [RHEL--quickstart-install-connect-red-hat.md), [SLES--quickstart-install-connect-suse.md), or [Ubuntu--quickstart-install-connect-ubuntu.md).
  * SQL Server 2017 RC2 [command-line tools--sql-server-linux-setup-tools.md).

**Create a backup on Windows**


There are several ways to create a backup file of a database on Windows. The following steps use SQL Server Management Studio (SSMS).

1. Start **SQL Server Management Studio** on your Windows machine.

1. In the connection dialog, enter **localhost**.

1. In Object Explorer, expand **Databases**.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### 6. &nbsp; [Release notes for SQL Server 2017 on Linux](sql-server-linux-release-notes.md)

*Updated: 2017-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_5) | [Next](#TitleNum_7))

<!-- Source markdown line 31.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4c8b9876f4792782314ba2f9b246405fb8036f84 acb97cf0a2e0bdd039575eaab9c41003316cbb02  (PR=2939  ,  Filename=sql-server-linux-release-notes.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



**<a id="RC2"></a> RC2 (August 2017)**


The SQL Server engine version for this release is 14.0.900.75.

**Supported platforms**


| Platform | File System | Installation Guide |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3 Workstation, Server, and Desktop | XFS or EXT4 | [Installation guide--quickstart-install-connect-red-hat.md) |
| SUSE Enterprise Linux Server v12 SP2 | EXT4 | [Installation guide--quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | EXT4 | [Installation guide--quickstart-install-connect-ubuntu.md) |
| Docker Engine 1.8+ on Windows, Mac, or Linux | N/A | [Installation guide--quickstart-install-connect-docker.md) |

> [!NOTE]
> You need at least 3.25GB of memory to run SQL Server on Linux.
> SQL Server Engine has been tested up to 1.5 TB of memory at this time.

**Package details**


Package details and download locations for the RPM and Debian packages are listed in the following table. Note that you do not need to download these packages directly if you use the steps in the following installation guides:

- [Install SQL Server package--sql-server-linux-setup.md)
- [Install Full-text Search package--sql-server-linux-setup-full-text-search.md)
- [Install SQL Server Agent package--sql-server-linux-setup-sql-agent.md)

| Package | Package version | Downloads |
|-----|-----|-----|
| Red Hat RPM package | 14.0.900.75-1 | [Engine RPM package](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-14.0.900.75-1.x86_64.rpm)</br>[High Availability RPM package](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-ha-14.0.900.75-1.x86_64.rpm)</br>[Full-text Search RPM package](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-fts-14.0.900.75-1.x86_64.rpm)</br>[SQL Server Agent RPM package](https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm) |



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### 7. &nbsp; [Installation guidance for SQL Server on Linux](sql-server-linux-setup.md)

*Updated: 2017-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_6) | [Next](#TitleNum_8))

<!-- Source markdown line 70.  ms.author= jroth.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00394e1733568a55243788d828968ff9b58a3c99 8ba2bf6f9cf4b5f54a6ee0f4d16d4437d5724880  (PR=2971  ,  Filename=sql-server-linux-setup.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=303d3b74da3fe370d19b7602c0e11e67b63191e7) -->



**<a id="rollback"></a> Rollback SQL Server**


To rollback or downgrade SQL Server to a previous release, use the following steps:

1. Identify the version number for the SQL Server package you want to downgrade to. For a list of package numbers, see the [Release notes--sql-server-linux-release-notes.md).

1. Downgrade to a previous version of SQL Server. In the following commands, replace `<version_number>` with the SQL Server version number you identified in step one.

   | Platform | Package update command(s) |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> It is only supported to downgrade to a release within the same major version, such as SQL Server 2017.

> [!IMPORTANT]
> Downgrade is only supported between RC2 and RC1 at this time.




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### 8. &nbsp; [Install SQL Server Integration Services (SSIS) on Linux](sql-server-linux-setup-ssis.md)

*Updated: 2017-08-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_7))

<!-- Source markdown line 66.  ms.author= lle.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a3fecd2553d1b25406445b8a26b22c9015dd98fe f836d560513fef1217e7dbce0ab85f78eec6f937  (PR=2948  ,  Filename=sql-server-linux-setup-ssis.md  ,  Dirpath=docs\linux\  ,  MergeCommitSha40=7b8c23474aee48e6d34ba268bc8942bc1c0263d3) -->



If you already have `mssql-server-is` installed, you can update to the latest version with the following command:

```
sudo apt-get install mssql-server-is
```


To remove `mssql-server-is`, you can run following command:
```
sudo apt-get remove msssql-server-is
```



**<a name="RHEL"></a> Install SSIS on RHEL**

To install the `mssql-server-is` package on RHEL, follow these steps:


1.  Enter superuser mode.

```
    sudo su
```


2.  Download the Microsoft SQL Server Red Hat repository configuration file.

```
    curl https://packages.microsoft.com/config/rhel/7/mssql-server.repo > /etc/yum.repos.d/mssql-server.repo
```


3.  Exit superuser mode.

```
    exit
```


4.  Run the following commands to install SQL Server Integration Services.

```
    sudo yum install -y mssql-server-is
```


5.  After installation, please run `ssis-conf`.







## Similar Articles

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

This section lists very similar articles for recently updated articles in other subject areas, within our public GitHub.com repository: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### Subject areas which do have new or recently updated articles

- [New + Updated (3+12) : **Advanced Analytics for SQL** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (5+0)  : **Connect to SQL** docs](../connect/new-updated-connect.md)
- [New + Updated (5+1)  : **Database Engine for SQL** docs](../database-engine/new-updated-database-engine.md)
- [New + Updated (19+82): **Integration Services for SQL** docs](../integration-services/new-updated-integration-services.md)
- [New + Updated (1+8)  : **Linux for SQL** docs](../linux/new-updated-linux.md)
- [New + Updated (12+1) : **Relational Databases for SQL** docs](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (0+1)  : **Reporting Services for SQL** docs](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (7+1)  : **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [New + Updated (1+1)  : **SQL Server Data Tools (SSDT)** docs](../ssdt/new-updated-ssdt.md)
- [New + Updated (0+2)  : **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [New + Updated (1+4)  : **SQL Server Management Studio (SSMS)** docs](../ssms/new-updated-ssms.md)
- [New + Updated (4+1)  : **Transact-SQL** docs](../t-sql/new-updated-t-sql.md)
- [New + Updated (0+1)  : **Tools for SQL** docs](../tools/new-updated-tools.md)

#### Subject areas which have no new or recently updated articles

- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **PowerShell for SQL** docs](../powershell/new-updated-powershell.md)
- [New + Updated (0+0): **Samples for SQL** docs](../sample/new-updated-sample.md)
- [New + Updated (0+0): **XQuery for SQL** docs](../xquery/new-updated-xquery.md)


