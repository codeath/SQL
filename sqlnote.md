SQL(Structured Query Language) 是一种ANSI(American National Standards Institute)标准的计算机语言    

SQL can do:
* SQL可以创建新的数据库及其对象（表，索引，视图，存储过程，函数和触发器）。    
* SQL可以修改现有数据库的结构。    
* SQL可以从数据库中删除（删除）对象。       
* SQL可以TRUNCATE（删除）表中的所有记录。    
* SQL可以对数据字典进行COMMENT。    
* SQL可以RENAME一个对象。    
* SQL可以从数据库中选择（检索）数据。   
* SQL可以将数据插入到表中。    
* SQL可以更新表中的现有数据。   
* SQL可以从数据库表中删除记录。    
* SQL可以在数据库中设置用户的GRANT和REVOKE权限。      

JDBC：在idea环境下使用mysql：
1、配置本地mysql server环境：下载  [MySQL]<https://dev.mysql.com/downloads/file/?id=476477/> 安装选项选择customer，里面包含有connector/J和
其它一些扩展工具,这个也可以单独下载，安装完成后可以在本地启动mysql服务。    
2、配置工程的mysql环境：在上面的安装目录下有个mysql-connector-java-xxx.jar这个jar包，在需要sql的project中选择：Project Structure -> Platform
Settings -> SDKS(下面是工程依赖的java类库|）->Classpath下选择右侧"+" -> Select Path(选中上述的安装目录下的jar包) ->ok 即可    
3、配置database：选择右侧的database -> " + " data source -> MySQL 填写完成基本信息 测试connection 连接上即可    
4、代码部分：    
<pre><code>
import java.sql.*;

public class TestJDBC {
    public static void main(String[] args) {
               Connection conn = null;
        Statement statement = null;
        ResultSet res = null;
        String url = "jdbc:mysql://localhost:3306/world";

        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection(url,"root","021874");
            statement = conn.createStatement();
            res = statement.executeQuery("select * from user");
            while (res.next()){
                res.getString("name");
                res.getInt("age");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            try {
                if (res != null) {
                    res.close();
                    res = null;
                } 
                if (statement != null){
                    statement.close();
                    statement = null;
                }
                if (conn != null) {
                    conn.close();
                    conn = null;
                }
            } catch (SQLException e){
                e.printStackTrace();
            }
        }
    }
}
</code></pre>
运行工程 "Process finished with exit code 0" 说明可以对指定数据库进行增删改查    
crash ：    
>* Establishing SSL connection without server's identity verification is not recommended. 
>>* 解决办法："jdbc:mysql://localhost:3306/world?useSSL=false"
>* The server time zone value 'ÖÐ¹ú±ê×¼Ê±¼ä' is unrecognized or represents more than one time zone.
>>* 解决办法："jdbc:mysql://localhost:3306/world?useSSL=false&serverTimezone=UTC"


