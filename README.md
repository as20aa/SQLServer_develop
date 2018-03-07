# SQLServer_develope
一个安装SQL Server和用c#进行开发的教程
## 开发前的准备工作
* 所需软件列表为（请看完这一part后再下载安装）    
visual studio    
SQL Server(developer版，商业版付费，express版也免费但是没有尝试过)    
SQL Server Management Studio (SSMS)(可选)    
下载安装连接：[visual studio](https://www.visualstudio.com/zh-hans/?rr=https%3A%2F%2Fwww.bing.com%2F)
[SQL Server developer版](https://www.microsoft.com/zh-cn/sql-server/sql-server-downloads)
[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)
下载和安装的是visual studio 2017和SQL Server这两个软件，下面的SQL Server Managment Studio是可选的，即可以安装也可以不要，只装下面那个是没任何用的，下面那个是数据库管理软件，真正的数据库服务都在SQL Server上。安装SQL Server时需要选择所需安装的功能和组件建议除了机器学习的模块之外全选。另外安装过程中会要求创建一个实例，请记住你的实际的名字，账号和密码，后面开发要用到       
建议下载安装介质，防止第一次安装中出现各种问题
* 安装完成之后确保SQL Server服务已启动，否则SQL Server Management Studio可能会登陆失败，可以在服务中查看是否有运行（因为我为了节约资源，所有的服务都选了手动启动），如若没有运行可以在以下目录找到sqlser程序，并运行   
路径：C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Binn （举个例子而已，实际路径可能不同）  
* 关于防火墙的设置
[如遇到防火墙阻挡，见链接](https://docs.microsoft.com/zh-cn/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access)
## 开始开发
* [开发简化流程](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/win/)   
* 一些说明    
开发示例第二步代码中的
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
数据库的所有代码都是不区分大小写的，所以在其他教程上看到的有大小写都是无用的，简单点就全大写或者全小写
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
* 查询表中的特定列的数据
```SQL
select * from tablename where 列名 = 键值
```
当然还有其他的查询方法，不限于这一种
* 查询是否存在指定数据库，如果不存在则新建一个
```SQL
create database if no exists 数据库名
```
