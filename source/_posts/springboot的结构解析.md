---
title: springboot的结构解析
date: 2025-04-21 16:25:45
tags:
    -springboot
categories: 学习
description: springboot的结构解析的一些分析
---
# springboot的结构解析



三层架构

为什么要分，把每个业务交给专门的层来处理，便于后期的维护，需求的增删等

![image-20250413170450206](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/20250413170450306.png)



![image-20250413170954939](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/20250413170954993.png)





## 1、controller层

```
仅仅只接收数据和传递数据，不做业务逻辑的处理，所有的controller都这样就三步。

例如
@PostMapping("/login")
    public Result<String> login(@RequestBody Map<String, Object> requestData) {
        // 1. 提取请求参数
        String username = (String) requestData.get("username");
        String password = (String) requestData.get("password");

        // 2. 调用 Service 层处理登录逻辑
        String token = userService.login(username, password);

        // 3. 返回响应
        if (token != null) {
            return Result.success(token);
        } else {
            return Result.error("Invalid username or password");
        }
    }
```



## 2、service层

```
实现业务功能的一层，很重要的一层
这里要先建立一个service对应的接口，在Impl下具体的实现方式。impl下是把每个功能单独拆开，前面写一个大函数将业务逻辑实现汇总。

例如
@Service
public class UserServiceImpl implements IUserService {

    @Autowired
    private UserMapper userMapper;

    @Autowired
    private RedisService redisService;

    // 大函数 1：实现登录功能
    @Override
    public String login(String username, String password) {
        // 协调各个子功能
        String encryptedPassword = encryptPassword(password); // 小函数 1：加密密码
        User user = validateUser(username, encryptedPassword); // 小函数 2：验证用户
        if (user == null) {
            return null;
        }
        return getOrGenerateToken(user); // 小函数 3：获取或生成 token
    }


    // 小函数 1：加密密码
    private String encryptPassword(String password) {
        return Md5Util.getMD5String(password);
    }


    // 小函数 2：获取或生成 token
    private String getOrGenerateToken(User user) {
        String username = user.getUsername();
        String token = getTokenFromRedis(username); // 小函数 3.1
        if (token != null) {
            return token;
        }
        return generateAndStoreToken(user); // 小函数 3.2
    }
    
    。。。。。。。。。。。
```



## 3、dao层

```
就是与数据库之间进行curd操作，也是mapper层。一个sql语言，一个函数处理

例如
@Mapper
public interface LoginMapper {

    @Select("SELECT id FROM login WHERE username = #{username} AND password = #{password} LIMIT 1")
    Integer exists(@Param("username") String username, @Param("password") String password);

    @Select("select * from login where id = #{id}")
    public Login findById(Integer id);

    @Update("update login set password = #{newPwd} where id = #{id}")
    void updataPwd(Integer id, String newPwd);
}

```



## 4、entity实体类

```
这个没什么好说的了，就是一些数据的类。对应数据库当中的表的字段，一一对应的嘛这个是pojo。这里注意一下和DOT的区分。POJO是映射数据库表结构，字段与表列一一对应（比如 User 类的 id、username、password、createdAt、updatedAt）。可能包含敏感字段（比如 password），不适合直接返回给前端。DTO：根据接口需求定义字段（比如 LoginResponseDTO 只包含 username 和 id）。适合返回给前端，不包含敏感字段。

例如
public class Login {
    private Integer id;
    private String username;
    private String password;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
    。。。。。。。。。。
```

