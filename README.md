# SQLServer_develope
一个安装SQL Server和用c#进行开发的教程
## 开发前的准备工作
* [下载和安装](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/win/)   
这里的对SQL Server的开发用到的是SQL Server 2017 Developer版本(默认是安装了visual studio 2017)    
安装功能时建议除了机器学习的模块之外全选    
建议下载安装介质，防止第一次安装中出现各种问题
* 安装SQL Server Management Studio (SSMS)（可选，如果不需要太高级的GUI管理功能可以忽略）
[安装链接](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)
* 安装完成之后需要先启动SQL Server服务，可以在服务中查看是否有运行（因为我为了节约资源，所有的服务都选了手动启动），如若没有运行可以在以下目录找到sqlser程序，并运行   
路径：C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn   
* 关于防火墙的设置
[如遇到防火墙阻挡，见链接](https://docs.microsoft.com/zh-cn/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access)
## 开始开发
[开发示例](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/win/step/2.html)
* 一些说明    
开发示例代码中的
```c++
SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
builder.DataSource = "DESKTOP-OA6B8Q0";   // 服务器名称
builder.UserID = "sa";              // 创建时使用的混合验证中的SQL Server账号名称   
builder.Password = "1234";      // SQL Server账号密码
builder.InitialCatalog = "master";
```
里面的参数选项均是在安装SQL Server时设置的参数，DataSource是创建的数据库的名称,UserID是创建混合验证模式时创建的用户，Password则是相应的密码
## 如何利用C#代码对SQL Server进行操作
[语言参考](https://docs.microsoft.com/zh-cn/sql/t-sql/new-updated-t-sql)
## 如何确认SQL Server中是否存在数据库、表等
[教程](www.cnblogs.com/for917157ever/archive/2012/04/19/2456826.html)
## 常见操作需求
* 查询当前所有数据库，并获得一张存储了所有数据的名字的表格
```SQL
select name from master..sysdatabases order by name;
```
这里的master..sysdatabases并非是固定的，而是依照当前登陆的分支来决定的，即Initcatalog参数，例如，登陆时登陆的是branch分支，则master..sysdatabases就要改为branch..sysdatabases，以此类推
* 查询当前数据库的下的所有表格
```SQL
select name from databasename..sysobjects order by name;
```
此处的databasename也跟上面的一样，database是使用的数据
