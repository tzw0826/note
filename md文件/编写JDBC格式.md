```java
/**
1、解决SQL注入问题
  	  只要用户提供的信息不参与SQL语句的编译过程，问题就解决了。
  	  即使用户提供的信息中含有SQL语句的关键字，但是没有参与编译，就不会起作用。
  	  要想用户信息不参与SQL语句的编译，那么就必须使用java.sql.PreparedStatement.
  	  PreparedStatement接口继承了java.sql.Statement
  	  PreparedStatement是属于编译的数据库操作对象。
  	  PreparedStatement的原理是：预先对SQL语句的框架进行编译，然后给SQL语句传"值"。


*/
public class JDBC{
    public static void main(String[] args){
        //初始化一个界面
        Map<String,String> userLoginInfo =  initUI();
        //验证用户名和密码
        boolean loginSuccess = login(userLoginInfo);
        //最后输出结果
        System.out.println(loginSuccess ? "登录成功":"登录失败");
    }
    private static boolean login(Map<String,String> userLoginInfo){
        //打标记的意识
        boolean loginSuccess = false;
        //单独定义变量
        String loginName = userLoginInfo.get("loginName");
        String loginPassword = userLoginfo.get("loginPassword");
        
        //JDBC代码
		Connection conn = null;
        PreparedStatement ps = null; //这里使用PreparedStatement，预编译的数据库操作对象
        ResultSet rs = null;
        
        try{
            //1、注册驱动
            class.forName("com.mysql.jdbc.Driver");
            //2、获取连接
   conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/books","root","0826");
           //将JDBC自动提交机制改为手动提交
            conn.setAutoCommit(false);//开启事务
            //3、获取预编译的数据库操作对象
            //sql语句的框子。其中一个?，表示一个占位符，一个?将来接收一个“值”，注意：占位符不能用				//单引号括起来。
           String sql = "select * from t_user where loginName = ? and loginPassword = ?";
           //初始化sql语句
            ps = conn.preparenStatement(sql);
            //给占位符?传值（第一个问号下标是1，第二个问号下标是2，JDBC中所有下标从1开始）
            ps.setString("张灵风","123");
            //4、执行sql
            rs = ps.executeQuery();
            //5、处理结果集
            if(rs.next()){
                //登录成功
				loginSuccess = true;
            }
            conn.commit();//提交事务
        }catch(Exception e){
            //回滚代码
            if(conn != null){
                conn.rollback();
            }
            e.printStackTrace();
        }finally{
            //释放资源
            if(rs != null){
                try{
                  rs.close();  
                }catch(SQLException e){
                    e.printStackTrace();
                }
                if(ps != null){
                try{
                  ps.close();  
                }catch(SQLException e){
                    e.printStackTrace();
                }
                    if(conn != null){
                try{
                  conn.close();  
                }catch(SQLException e){
                    e.printStackTrace();
                }
            }
        }
        
    }
} 
```



**Statement 和 PreparedStatement的区别？**

1. Statement存在sql注入问题，PreparedStatement解决了sql注入问题。
2. Statement是编译一次执行一次。PreparedStatement是编译一次，可执行n次。PreparedStatement效率高一些。
3. PreparedStatement会在编译阶段做类型的安全检查。



**JDBC事务处理的重要三行代码：**

1. conn.setAutoCommit(false);
2. conn.commit();
3. conn.rollback();



