---
title: BizTalk Server MessageBox 数据库文件组 SQL 脚本 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: af4fe437-41ca-46c1-90eb-a28ed73312b6
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d80d5aeb35c27a04f637f4e5ca466996855f35fb
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36973062"
---
# <a name="biztalk-server-messagebox-database-filegroups-sql-script"></a>BizTalk Server MessageBox 数据库文件组 SQL 脚本
本主题提供了可以在 BizTalk Server 环境中创建多个文件和文件组的 BizTalk MessageBox 数据库中的 SQL Server 实例运行的 SQL 脚本。  
  
> [!IMPORTANT]
>  提供"按原样，"用于演示或培训目的，并且将使用您自己承担，此脚本。 使用此脚本不受 Microsoft，因此 Microsoft 不保证此脚本的适用性。  
> 
> [!IMPORTANT]
>  使用此 SQL 脚本来创建多个文件和文件组为 BizTalk MessageBox 数据库时，应考虑以下事项：  
> 
> 1. **重新运行在以下情况下的 MessageBox 数据库文件组 SQL 脚本：**  
> 
>    - 如果安装运行的 BizTalk Server 修补程序或 service pack **msgboxlogic.sql**，将需要再次运行的 MessageBox 数据库文件组 SQL 脚本。 这是必需的因为 msgboxlogic.sql 还原 MessageBox 文件组和文件复制到默认设置，即使用主文件组。 若要确定是否修补程序或服务包运行 msgboxlogic.sql，检查**文件信息**修补程序 KB 文章的部分。 或检查 setup.xml 文件所包含的服务包文件。  
>    - 如果您添加到 BizTalk Server 组新的主机，将需要再次运行 MessageBox 数据库文件组 SQL 脚本。 这是必需的因为存储的过程创建新主机配置为主机默认使用的主文件组的表。  
>    - **在多 MessageBox 环境中应用 MessageBox 数据库文件组 SQL 脚本：** 但不是必需的可以对在多 Messagebox 环境中每个 MessageBox 执行 MessageBox 数据库文件组 SQL 脚本。  
  
## <a name="biztalk-messagebox-database-filegroups-sql-script"></a>BizTalk MessageBox 数据库文件组 SQL 脚本  
 可以使用以下 SQL 脚本来创建多个文件和文件组主题中所述[优化文件组的数据库 2](../technical-guides/optimizing-filegroups-for-the-databases2.md)。  
  
```  
/************************************************************  
This script will create multiple filegroups / files for the  
BizTalk MessageBox database. It will also set the initial  
size, location, and the number of files per filegroup before  
distributing objects among them.  
  
************************************************************/  
  
USE BizTalkMsgBoxDb  
GO  
SET NOCOUNT ON  
GO  
  
/************************************************************  
Declare Variables  
************************************************************/   
DECLARE   
      @FILES_PER_FILEGROUP              tinyint,  
      @INITIAL_FILE_SIZE                nvarchar(50),  
      @GROWTH_INCREMENT                 nvarchar(50),  
      @MISC_DATA_FILE_PATH              nvarchar(200),  
      @MISC_IDXS_FILE_PATH              nvarchar(200),  
      @PREDICATE_DATA_FILE_PATH         nvarchar(200),  
      @PREDICATE_IDXS_FILE_PATH         nvarchar(200),  
      @MESSAGE_DATA_FILE_PATH           nvarchar(200),  
      @MESSAGE_INSTANCE_FILE_PATH       nvarchar(200),  
      @MESSAGE_IDXS_FILE_PATH           nvarchar(200),  
      @SQLCmd                           nvarchar(2000),  
      @DBNAME                           sysname,  
      @OBJECT_ID                        int,  
      @UNDO                             bit,  
      @PRIMARY_FILE_GROUP               sysname,  
      @FILE_GROUP                       sysname,  
      @FILE_GROUP_ID                    int,  
      @FILE_PATH                        nvarchar(200),  
      @DEFAULT_FILE_PATH                nvarchar(200),  
      @FILE_NAME                        nvarchar(200),  
      @FULL_NAME                        nvarchar(200),  
      @FILE_COUNT                       tinyint,  
      @COUNTER                          int,  
      @DEFAULT_FILEGROUP                nvarchar(50)  
  
/************************************************************  
Declare/Create Tables  
************************************************************/   
Declare @FILE_GROUP_TABLE table   
          (  
          name sysname,  
          file_count tinyint,   
          file_path nvarchar(1024)  
          )  
Declare @TABLE_ALLOCATIONS table   
          (  
          table_name sysname,   
          main_file_group nvarchar(1024),   
          ncindex_file_group nvarchar(1024)  
          )  
  
/************************************************************  
Set User-defined Variables  
************************************************************/  
--Set to 0, this varibale has no effect,   
--Set to 1 to undo changes and move all objects back to Primary filegroups, and delete all empty data files/filegroups  
SET @UNDO = 0  
--Set to the number of data files to be created per filegroup  
SET @FILES_PER_FILEGROUP = 1  
--Set to the initial file size per data file in MB - eg: '100MB'  
SET @INITIAL_FILE_SIZE = N'50MB'  
--Set to the Growth Increment per data file in MB - eg: '100MB'  
SET @GROWTH_INCREMENT = N'50MB'  
--The following 7 Variables should be set to the paths for each filegroup - eg: C:\Data\  
SET @MISC_DATA_file_path ='C:\DATA\'  
SET @MISC_IDXS_file_path ='C:\DATA\'  
SET @PREDICATE_DATA_file_path ='C:\DATA\'  
SET @PREDICATE_IDXS_file_path ='C:\DATA\'  
SET @MESSAGE_DATA_file_path     ='C:\DATA\'  
SET @MESSAGE_INSTANCE_file_path     ='C:\DATA\'  
SET @MESSAGE_IDXS_file_path     ='C:\DATA\'  
--Set Database Name Variable  
SET @DBNAME = DB_NAME()  
--Set Default FileGroup Variable  
SET @DEFAULT_FILEGROUP = 'MISC_DATA'  
  
/************************************************************  
If resetting the object distribution, set the Primary  
filegroup as the default  
************************************************************/  
If @UNDO = 1   
BEGIN  
     if not exists(SELECT TOP 1 groupname FROM  sys.sysfilegroups WHERE (status & 0x10 > 0) and groupname = 'PRIMARY')  
     BEGIN  
          SET @DEFAULT_FILEGROUP = 'PRIMARY'  
          exec ('ALTER DATABASE ' + @DBNAME + ' MODIFY FILEGROUP [' + @DEFAULT_FILEGROUP + '] DEFAULT')  
     END  
END  
  
/************************************************************  
Find path of data file in the default filegroup to use   
until we set our user-defined paths - used when 'Undoing'  
************************************************************/  
SELECT TOP 1 @PRIMARY_FILE_GROUP = sfg.groupname, @FILE_NAME = sf.name, @FULL_NAME = sf.filename   
FROM sys.sysfiles sf, sys.sysfilegroups sfg  
WHERE (sfg.status & 0x10 > 0)  
     AND sf.groupid = sfg.groupid  
  
--Find and set our default file path variable  
SET @COUNTER = CHARINDEX(@FILE_NAME, @FULL_NAME)  
SET @DEFAULT_FILE_PATH = SUBSTRING(@FULL_NAME, 1, @COUNTER - 1)  
  
/************************************************************  
Populate a temporary table with a list of filegroups   
we want to create, their paths and the number  
of data files to create per filegroup  
************************************************************/  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'MISC_DATA', @FILES_PER_FILEGROUP, @MISC_DATA_file_path)  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'MISC_INDEXES', @FILES_PER_FILEGROUP, @MISC_IDXS_file_path)  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'PREDICATE_DATA', @FILES_PER_FILEGROUP, @PREDICATE_DATA_file_path)  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'PREDICATE_INDEXES', @FILES_PER_FILEGROUP, @PREDICATE_IDXS_file_path)  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'MESSAGE_DATA', @FILES_PER_FILEGROUP, @MESSAGE_DATA_file_path)  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'MESSAGE_INSTANCES', @FILES_PER_FILEGROUP, @MESSAGE_INSTANCE_file_path)  
INSERT INTO @file_group_table (name, file_count, file_path) VALUES (N'MESSAGE_INDEXES', @FILES_PER_FILEGROUP, @MESSAGE_IDXS_file_path)  
  
/************************************************************  
Populate a temporary table with a list of  
table and filegroup associations  
************************************************************/  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ActiveRefCountLog', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'AddRef', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ApplicationProps', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Applications', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'BitwiseANDPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'BizTalkDBVersion', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ConvoySetInstances', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ConvoySets', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'EqualsPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'EqualsPredicates2ndPass', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ExistsPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'FirstPassPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Fragments', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'GreaterThanOrEqualsPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'GreaterThanPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Instances', N'MESSAGE_INSTANCES', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'InstancesOperatedOn', N'MESSAGE_INSTANCES', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'InstancesPendingOperations', N'MESSAGE_INSTANCES', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'InstancesSuspended', N'MESSAGE_INSTANCES', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'LessThanOrEqualsPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'LessThanPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'LocalizedErrorStrings', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MarkLog', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessageParts', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessagePredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessageProps', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessageRefCountLog1', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessageRefCountLog2', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessageRefCountLogTotals', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'MessageZeroSum', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Modules', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'NotEqualsPredicates', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'OperationsProgress', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PartRefCountLog1', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PartRefCountLog2', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PartRefCountLogTotals', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Parts', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PartZeroSum', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PredicateGroup', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PredicateGroupNames', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PredicateGroupZeroSum1', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'PredicateGroupZeroSum2', N'PREDICATE_DATA', N'PREDICATE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ProcessHeartbeats', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Release', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'ServiceClasses', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Services', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Spool', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'StaticStateInfo', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Subscription', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Tracking_Fragments1', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Tracking_Fragments2', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Tracking_Parts1', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Tracking_Parts2', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Tracking_Spool1', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'Tracking_Spool2', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_0_0', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_0_1', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_0_2', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_0_3', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_1_0', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_1_1', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_1_2', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingData_1_3', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingDataPartitions', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingMessageReferences', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrackingSpoolInfo', N'MESSAGE_DATA', N'MESSAGE_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TruncateRefCountLog', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'TrustedUsers', N'MISC_DATA', N'MISC_INDEXES')  
INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES (N'UniqueSubscription', N'MISC_DATA', N'MISC_INDEXES')  
  
/************************************************************  
Find our BizTalk Host specific tables and add them into  
our temporary table  
************************************************************/  
declare @nvcAppName nvarchar(256)  
declare applications_cursor cursor FAST_FORWARD FOR   
SELECT nvcApplicationName FROM Applications  
  
OPEN applications_cursor  
FETCH NEXT FROM applications_cursor INTO @nvcAppName  
WHILE (@@FETCH_STATUS = 0)  
BEGIN   
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[' + @nvcAppName + N'Q]', N'MISC_DATA', N'MISC_INDEXES')  
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[' + @nvcAppName + N'Q_Scheduled]', N'MISC_DATA', N'MISC_INDEXES')  
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[' + @nvcAppName + N'Q_Suspended]', N'MISC_DATA', N'MISC_INDEXES')  
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[InstanceStateMessageReferences_' + @nvcAppName + N']', N'MISC_DATA', N'MISC_INDEXES')  
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[DynamicStateInfo_' + @nvcAppName + N']', N'MISC_DATA', N'MISC_INDEXES')  
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[' + @nvcAppName + N'_MessageRefCountLog]', N'MISC_DATA', N'MISC_INDEXES')  
     INSERT INTO @table_allocations (table_name, main_file_group, ncindex_file_group) VALUES ('[' + @nvcAppName + N'_DequeueBatches]', N'MISC_DATA', N'MISC_INDEXES')  
  
     FETCH NEXT FROM applications_cursor INTO @nvcAppName  
END  
CLOSE applications_cursor  
DEALLOCATE applications_cursor  
  
/************************************************************  
Loop through our temporary table of filegroups   
and create them  
************************************************************/  
DECLARE file_group_cursor CURSOR FAST_FORWARD FOR  
SELECT name, file_count, file_path FROM @file_group_table  
  
OPEN file_group_cursor  
FETCH NEXT FROM file_group_cursor INTO @file_group, @file_count, @file_path  
WHILE ( (@@FETCH_STATUS = 0) AND (@UNDO = 0) )  
BEGIN  
     SET @file_group_id = FILEGROUP_ID(@file_group)  
  
     /************************************************************  
     Create Filegroup if it does not already exist  
     ************************************************************/  
     IF (@file_group_id IS NULL)  
     BEGIN  
          exec('ALTER DATABASE [' + @DBNAME + '] ADD FILEGROUP [' + @file_group + ']')  
     END  
  
     print 'Creating FileGroup: ' + @file_path + @file_group  
  
     /************************************************************  
     Loop through each new filegroup and create the data file  
     for the filegroup if one does not exist  
     ************************************************************/  
     SET @file_group_id = FILEGROUP_ID(@file_group)  
     IF NOT EXISTS (SELECT TOP 1 groupid FROM sys.sysfiles WHERE groupid = @file_group_id)  
     BEGIN  
          set @COUNTER = 0  
          WHILE (@COUNTER < @file_count)  
          BEGIN  
               if @COUNTER = 0  
               BEGIN  
                    SET @file_name = @DBNAME + '_' + @file_group  
               END  
               ELSE   
                    SET @file_name = @DBNAME + '_' + @file_group + '_' + CAST(@COUNTER as nvarchar(3))  
  
               SET @full_name = @file_path + @file_name + '.ndf'  
  
               print 'Creating Data File: ' + @full_name + ' in ' + @file_group  
  
               --Build our TSQL string to add our data file to the database  
               SET @SQLCmd = N'ALTER DATABASE [' + @DBNAME + '] ADD FILE (   
                                             NAME = N''' + @file_name + ''',  
                                             FILENAME = N''' + @full_name + ''' ,  
                                             SIZE = ' + @INITIAL_FILE_SIZE + ',  
                                             MAXSIZE = UNLIMITED,   
                                             FILEGROWTH = '+ @GROWTH_INCREMENT +' )   
                                        TO FILEGROUP [' + @file_group + ']'  
               --Execute our TSQL string  
               EXECUTE (@SQLCmd)  
  
               /************************************************************  
               Set the requested Filegroup to be the default  
               ************************************************************/  
               If @file_group = @DEFAULT_FILEGROUP  
               Begin  
                    --Build our TSQL string to set requested FileGroup as default  
                    SET @SQLCmd = N'ALTER DATABASE [' + @DBNAME + '] MODIFY FILEGROUP ' + @file_group + ' DEFAULT'  
                    print 'Changing ' + @file_group + ' FileGroup to DEFAULT'  
                    --Execute our TSQL string  
                    EXECUTE (@SQLCmd)  
               END  
  
               set @COUNTER = @COUNTER + 1  
          END  
     END  
  
     FETCH NEXT FROM file_group_cursor INTO @file_group, @file_count, @file_path  
END  
CLOSE file_group_cursor  
  
/************************************************************  
Loop through our temporary table of table and filegroup  
allocations and recreate clustered and non-clustered indexes  
on the New Filegroups as well as move heaps to their new  
filegroup.  
************************************************************/  
declare @table_name sysname,  
          @index_name sysname,  
          @column_name sysname,  
          @column_order int,  
          @index_id int,  
          @is_unique bit,  
          @data_space_id int,  
          @ignore_dup_key bit,  
          @is_primary_key bit,  
          @is_unique_constraint bit,  
          @fill_factor tinyint,  
          @is_padded bit,  
          @is_disabled bit,  
          @allow_row_locks bit,  
          @allow_page_locks bit,  
          @ncindex_file_group nvarchar(1024),  
          @ncindex_file_group_id int,  
          @create_index_sql nvarchar(4000)  
  
DECLARE table_allocations_cursur CURSOR FAST_FORWARD FOR  
SELECT table_name, main_file_group, ncindex_file_group FROM @table_allocations  
OPEN table_allocations_cursur  
FETCH NEXT FROM table_allocations_cursur INTO @table_name, @file_group, @ncindex_file_group  
WHILE (@@FETCH_STATUS = 0)  
BEGIN  
          /************************************************************  
          If reverting back to single filegroup, then overwrite  
          filegroups with 'PRIMARY'  
          ************************************************************/  
          if (@UNDO = 1)  
          BEGIN  
               set @file_group = @primary_file_group  
               set @ncindex_file_group = @primary_file_group  
          END  
          else if (@ncindex_file_group is null)  
          BEGIN  
               SET @ncindex_file_group = @file_group  
          END  
  
          set @file_group_id = FILEGROUP_ID(@file_group)  
          set @ncindex_file_group_id = FILEGROUP_ID(@file_group)  
          select @object_id = OBJECT_ID(@table_name)  
  
          /************************************************************  
          Get data on the clustered and non clustered indexes   
          for the current table.  
          ************************************************************/  
          IF (@object_id is not null)  
          BEGIN  
               DECLARE table_indexes_cursor CURSOR FAST_FORWARD FOR  
               SELECT name, index_id, is_unique, data_space_id, ignore_dup_key, is_primary_key, is_unique_constraint, fill_factor, is_padded, is_disabled, allow_row_locks, allow_page_locks  
                    FROM sys.indexes WHERE object_id = @object_id AND (type = 0 OR type = 1 OR type = 2)  
                    ORDER BY name, index_id ASC  
  
               OPEN table_indexes_cursor  
               FETCH NEXT FROM table_indexes_cursor INTO @index_name, @index_id, @is_unique, @data_space_id, @ignore_dup_key, @is_primary_key, @is_unique_constraint, @fill_factor, @is_padded, @is_disabled, @allow_row_locks, @allow_page_locks  
               WHILE (@@FETCH_STATUS = 0)  
               BEGIN  
                    /************************************************************  
                    Are we dealing with a HEAP? ie Index_id = 0  
                    If so, we need to create a temporary clustered index on   
                    new filegroup to move the table before deleting this  
                    clustered index  
                    ************************************************************/  
                    if @index_id = 0   
                    BEGIN  
                         /************************************************************  
                         If dealing with a HEAP...  
                         Create temp Clustered Index to move data  
                         ************************************************************/  
                         SET @create_index_sql = 'CREATE CLUSTERED INDEX TEMP_CIX ON ' + @table_name + '('  
                         select @column_name = name from sys.columns where object_id = @object_id and column_id = 1   
                         SET @create_index_sql = @create_index_sql + @column_name + ') ON [' + @file_group + ']'  
                         print 'Create TEMP Clustered index TEMP_CIX on table ' + @table_name + ' on FileGroup ' + @file_group  
                         exec (@create_index_sql)  
  
                         /************************************************************  
                         Delete temp Clustered Index  
                         ************************************************************/  
                         SET @create_index_sql = 'DROP INDEX TEMP_CIX ON ' + @table_name   
                         print 'Drop TEMP Clustered index TEMP_CIX from table '+@table_name + 'on FileGroup ' + @file_group  
                         exec (@create_index_sql)  
                    END  
  
                    /************************************************************  
                    Deal with the clustered or non clustered indexes  
                    ************************************************************/  
                    if ( ( (@index_id = 1) AND (@data_space_id != @file_group_id) ) OR  
                          ( (@index_id > 1) AND (@data_space_id != @ncindex_file_group_id) ) )  
                    BEGIN  
  
                         /************************************************************  
                         Build string to recreate this index  
                         ************************************************************/  
                         SET @create_index_sql = 'CREATE '  
                         if (@is_unique = 1)  
                              SET @create_index_sql = @create_index_sql + 'UNIQUE '  
                         if (@index_id = 1)        
                              SET @create_index_sql = @create_index_sql + 'CLUSTERED '  
                         else                      
                              SET @create_index_sql = @create_index_sql + 'NONCLUSTERED '  
                         SET @create_index_sql = @create_index_sql + 'INDEX ' + @index_name + ' ON ' + @table_name + '('  
  
                         /************************************************************  
                         Get details of columns for this table  
                         ************************************************************/  
                         DECLARE index_columns_cursor CURSOR FAST_FORWARD FOR  
                         SELECT ic.key_ordinal, c.name FROM sys.columns c  
                              JOIN sys.index_columns ic ON ic.object_id = @object_id AND ic.index_id = @index_id AND c.column_id = ic.column_id  
                              WHERE c.object_id = @object_id  
                              ORDER BY ic.key_ordinal ASC  
  
                         OPEN index_columns_cursor  
                         FETCH NEXT FROM index_columns_cursor INTO @column_order, @column_name  
                         WHILE (@@FETCH_STATUS = 0)  
                         BEGIN  
                              if (@column_order > 1)  
                                   SET @create_index_sql = @create_index_sql + ', '  
                              SET @create_index_sql = @create_index_sql + @column_name       
                              FETCH NEXT FROM index_columns_cursor INTO @column_order, @column_name  
                         END  
                         CLOSE index_columns_cursor  
                         DEALLOCATE index_columns_cursor  
  
                         SET @create_index_sql = @create_index_sql + ') WITH ('  
                         if (@ignore_dup_key = 1)  
                              SET @create_index_sql = @create_index_sql + 'IGNORE_DUP_KEY = ON, '  
                         if (@allow_page_locks = 0)  
                              SET @create_index_sql = @create_index_sql + 'ALLOW_PAGE_LOCKS = OFF, '  
                         SET @create_index_sql = @create_index_sql + 'DROP_EXISTING = ON) '  
                         if (@index_id = 1)  
                              SET @create_index_sql = @create_index_sql + 'ON [' + @file_group + ']'  
                         else  
                              SET @create_index_sql = @create_index_sql + 'ON [' + @ncindex_file_group + ']'       
                         print @create_index_sql  
                         --Execute SQL string to recreate the index  
                         exec (@create_index_sql)  
                    END  
                    FETCH NEXT FROM table_indexes_cursor INTO @index_name, @index_id, @is_unique, @data_space_id, @ignore_dup_key, @is_primary_key, @is_unique_constraint, @fill_factor, @is_padded, @is_disabled, @allow_row_locks, @allow_page_locks  
               END  
               CLOSE table_indexes_cursor  
               DEALLOCATE table_indexes_cursor  
          END  
          FETCH NEXT FROM table_allocations_cursur INTO @table_name, @file_group, @ncindex_file_group  
END  
  
/************************************************************  
If we are setting everything back to a single filegroup  
we have to remove previously created files now that they  
are empty before we delete the empty filegroups  
************************************************************/  
if (@UNDO = 1)  
BEGIN  
     OPEN file_group_cursor  
     FETCH NEXT FROM file_group_cursor INTO @file_group, @file_count, @file_path  
  
     WHILE (@@FETCH_STATUS = 0)  
     BEGIN  
          SET @file_group_id = FILEGROUP_ID(@file_group)  
  
          IF (@file_group_id IS NOT NULL)  
          BEGIN  
               DECLARE files_in_group_cursor CURSOR FAST_FORWARD FOR  
               SELECT name FROM sys.sysfiles WHERE groupid = @file_group_id  
               OPEN files_in_group_cursor  
               FETCH NEXT FROM files_in_group_cursor INTO @file_name  
               WHILE (@@FETCH_STATUS = 0)  
               BEGIN  
                    exec('ALTER DATABASE [' + @DBNAME + '] REMOVE FILE [' + @file_name + ']')  
                    FETCH NEXT FROM files_in_group_cursor INTO @file_name  
               END  
  
               CLOSE files_in_group_cursor  
               DEALLOCATE files_in_group_cursor  
  
               exec('ALTER DATABASE [' + @DBNAME + '] REMOVE FILEGROUP [' + @file_group + ']')  
          END  
  
          FETCH NEXT FROM file_group_cursor INTO @file_group, @file_count, @file_path  
     END  
  
     /************************************************************  
     Truncate T-Log.  WITH TRUNCATE_ONLY not available from SQL Server  
     2008 therefore have to alter recovery model to simple,  
     issue a checkpoint, then change recovery model back to full  
     ************************************************************/  
     declare @Currentdbname sysname  
     set @Currentdbname = db_name()  
     declare @cmd varchar(1000)  
     SET @cmd = 'ALTER DATABASE ' + @Currentdbname + ' SET RECOVERY SIMPLE'  
     EXEC(@cmd)  
     print 'Set Recovery Model to Simple'  
     Checkpoint  
     print 'Perform CheckPoint'  
     SET @cmd = 'ALTER DATABASE ' + @DBNAME + ' SET RECOVERY FULL'  
     print 'Set Recovery Model back to Full'  
     EXEC(@cmd)  
  
     CLOSE file_group_cursor  
END  
  
DEALLOCATE file_group_cursor  
GO  
  
print '********Object to FileGroup Distribution Completed********'  
  
/************************************************************  
Verify that Distribution of tables among filegroups has   
completed successfully  
************************************************************/  
SELECT sysobjects.[name] AS TableName, sysindexes.[name], sysfilegroups.groupname AS FileGroupName,  
sysfiles.[filename] AS PhysicalFileName, sysfiles.[name] AS LogicalFileName  
FROM sysobjects   
JOIN sysindexes ON sysobjects.[id] = sysindexes.[id]   
JOIN sysfilegroups ON sysindexes.groupid = sysfilegroups.groupid   
JOIN sysfiles ON sysfilegroups.groupid = sysfiles.groupid   
where sysobjects.[name] not like 'sys%' and sysobjects.xtype = 'U'  
ORDER BY sysobjects.[name], sysindexes.[name]  
GO  
print '********Object to Filegroup Distribution Report Completed********'  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [优化数据库性能](../technical-guides/optimizing-database-performance.md)