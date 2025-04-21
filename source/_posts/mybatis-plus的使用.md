---
title: mybatis-plus的使用
date: 2025-04-21 16:25:12
tags:
    -springboot
    -mybatisplus
categories: 学习
description: mybatis-plus的使用
---

# mybatis-plus的使用

mp可以帮助我们快速完成项目的curd。

## 1、首先在配置中完成引用

![image-20250419151410087](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/20250419151410165.png)

在pom文件中添加如下依赖

```
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.5.5</version> <!-- 这里写你想用的版本 -->
        </dependency>
```

重新加载后即可，这里的话mybatisplus包含mybatis，可以只安装一个就行了。两个都安装也没啥。最好还是一个吧。

## 2、具体在项目中引用操作如下

![QQ截图20250419144911](https://zxztypora.oss-cn-hangzhou.aliyuncs.com/20250419151257396.png)

### （1）创建一个pojo和数据库表对接

pojo下面创建一个实体类对应数据库表

```
package org.example.mybatis.pojo;

public class Student {
    private Integer id;
    private String name;
    private Integer age;
    private Integer grade;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public Integer getGrade() {
        return grade;
    }

    public void setGrade(Integer grade) {
        this.grade = grade;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", grade=" + grade +
                '}';
    }
}

```

### （2）创建mapper

继承BaseMapper

```
package org.example.mybatis.dao;

import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import org.apache.ibatis.annotations.Mapper;
import org.example.mybatis.pojo.Student;

@Mapper
public interface StudentMapper extends BaseMapper<Student> {

}
```

### （3）创建service

继承IService

```
package org.example.mybatis.service;
import com.baomidou.mybatisplus.extension.service.IService;
import org.example.mybatis.pojo.Student;

public interface StudentService extends IService<Student> {
    // 你可以在这里加自定义方法，比如：
    // Student findByPhone(String phone);
}
```

### （4）创建serviceImpl

继承ServiceImpl

```
package org.example.mybatis.service.impl;

import com.baomidou.mybatisplus.extension.service.impl.ServiceImpl; // 这个导入漏了
import org.example.mybatis.dao.StudentMapper;
import org.example.mybatis.pojo.Student; // 记得导入 Student 实体类
import org.example.mybatis.service.StudentService;
import org.springframework.stereotype.Service;

@Service
public class StudentServiceImpl extends ServiceImpl<StudentMapper, Student> implements StudentService {
    // 这里可以加你自己的业务逻辑方法，比如：
    // public Student findByPhone(String phone) { ... }
}

```

### （5）在controller当中试一试

```
package org.example.mybatis.controller;
import org.example.mybatis.pojo.Student;
import org.example.mybatis.service.StudentService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class StudentController {

    @Autowired
    private StudentService studentService;

    @GetMapping("/findd")
    public Student find(@RequestParam int id) {
        return studentService.getById(id);  // 调用 Service 的 getById() 方法来查找学生
    }
}

```

