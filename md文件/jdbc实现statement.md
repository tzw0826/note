```java
import java.sql.Driver;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Connection;
import java.sql.Statement;

public class JDBCTest{
    public static void main(String[] args){
         Connection conn = null;
         Statement stmt = null;
        try{
            //1、注册驱动
            Driver driver = new com.mysql.jdbc.Driver(); //多态，父类型引用指向子类型对象。
            DriverManger.registerDriver(driver);
            //2、获取连接
            String url = "jdbc:mysql://127.0.0.1:3306/books";
            String user = "root";
            String password = "0826";
            conn = DriverManager.getConnection(url,user,password);
            //com.maysql.jdbc.JDBC4connection@41cf53f9
            System.out.println("数据库连接对象" + conn);
            //3、获取数据库操作对象（Statement专门执行sql语句的）
            //编译sql语句
            stmt = conn.createStatement();
            //4、执行sql
            Stirng sql = "insert into student(name,age) values('姓名','年龄')";
            //专门执行DML语句的（insert delete update）
            //返回值是“影响数据库中的记录条数”
            int count = stmt.executeUpdate(sql);            
        }catch(SQLException e){
            e.printStackTrace();
        }finally{
            //6、释放资源
            //为了保证资源一定释放，在finally语句块中关闭资源
            //并且要遵循从小到大依次关闭
            //分别对其try...catch
            try{
                if(stmt != null){
                    stmt.close();
                }
                if(conn != null){
                    conn.close();
                }
            }
        }
    }
}
```

