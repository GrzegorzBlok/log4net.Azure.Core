[![NuGet](https://img.shields.io/nuget/v/log4net.Appender.Azure.Core.svg?style=flat)](https://www.nuget.org/packages/log4net.Appender.Azure.Core/)

Transfer all your logs to the [Azure Table or Blob Storage](http://azure.microsoft.com/de-de/services/storage/) via Appender for [log4Net](https://logging.apache.org/log4net/)

## Install
Add To project via NuGet:  
1. Right click on a project and click 'Manage NuGet Packages'.  
2. Search for 'log4net.Appender.Azure.Core' and click 'Install'.  

## Configuration
### Table Storage 
Every log entry is stored in a separate row.

	<appender name="AzureTableAppender" type="log4net.Appender.Azure.Core.AzureTableAppender, log4net.Appender.Azure.Core">
	   <param name="TableName" value="testLoggingTable"/>
	   <!-- You can either specify a connection string or use the ConnectionStringName property instead -->
	   <param name="ConnectionString" value="UseDevelopmentStorage=true"/>
	   <!--<param name="ConnectionStringName" value="GlobalConfigurationString" />-->
	   <!-- You can specify this to make each LogProperty as separate Column in TableStorage, 
		Default: all Custom Properties were logged into one single field -->
	   <param name="PropAsColumn" value="true" />
	   <!-- You can specify this to make each LogProperty as separate Column in TableStorage, 
		Default: all Custom Properties were logged into one single field -->
	   <param name="PropAsColumn" value="true" />
	   <param name="PartitionKeyType" value="LoggerName" />
	   <layout type="log4net.Layout.PatternLayout">
	   	   <conversionPattern value="[%property{methodAndUri}] %method -- %message %exception" />
	   </layout>
	 </appender>
	
* <b>TableName:</b>  
  Name of the table in Table Storage
* <b>ConnectionString:</b>  
  the full Azure Storage connection string
* <b>ConnectionStringName:</b>  
  Name of a connection string specified under connectionString
* <b>PropAsColumn(optional):</b>  
  Default: all properties were written in a single field(default).  
  If you specifiy this with the value true then each custom log4net property is logged as separate column/field in the table.  
  Remember that Table storage has a Limit of 255 Properties ([see here](https://azure.microsoft.com/en-us/documentation/articles/storage-table-design-guide/#about-the-azure-table-service)).
* <b>PartitionKeyType(optional):</b>  
  Default "LoggerName": (each logger gets his own partition in Table Storage)  
  "DateReverse": order by Date Reverse to see the latest items first ([How to order elements by date reverse](http://gauravmantri.com/2012/02/17/effective-way-of-fetching-diagnostics-data-from-windows-azure-diagnostics-table-hint-use-partitionkey/))

	
### BlobStorage
Every log Entry is stored as separate XML file.

    <appender name="AzureBlobAppender" type="log4net.Appender.Azure.Core.AzureBlobAppender, log4net.Appender.Azure.Core">
      <param name="ContainerName" value="testloggingblob"/>
      <param name="DirectoryName" value="logs"/>
      <!-- You can either specify a connection string or use the ConnectionStringName property instead -->
      <param name="ConnectionString" value="UseDevelopmentStorage=true"/>
      <!--<param name="ConnectionStringName" value="GlobalConfigurationString" />-->
    </appender>
	
* <b>ContainerName:</b>  
  Name of the container in Blob Storage	
* <b>DirectoryName:</b>  
  Name of the folder in the specified container
* <b>ConnectionString:</b>  
  the full Azure Storage connection string
* <b>ConnectionStringName:</b>  
  Name of a connection string specified under connectionString

### AppendBlobStorage
Every log Entry is stored as separate XML file.

    <appender name="AzureAppendBlobAppender" type="log4net.Appender.Azure.Core.AzureAppendBlobAppender, log4net.Appender.Azure.Core">
      <param name="ContainerName" value="testloggingblob"/>
      <param name="DirectoryName" value="logs"/>
      <!-- You can either specify a connection string or use the ConnectionStringName property instead -->
      <param name="ConnectionString" value="UseDevelopmentStorage=true"/>
      <!--<param name="ConnectionStringName" value="GlobalConfigurationString" />-->
    </appender>
	
* <b>ContainerName:</b>  
  Name of the container in Blob Storage	
* <b>DirectoryName:</b>  
  Name of the folder in the specified container
* <b>ConnectionString:</b>  
  the full Azure Storage connection string
* <b>ConnectionStringName:</b>  
  Name of a connection string specified under connectionString
  
