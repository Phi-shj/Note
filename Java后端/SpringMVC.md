# SpringMVC

## 1.SpringMVC简介

### 1.1 MVC

是一种架构思想，不是框架或者设计模式

### 1.2 SpringMVC

是Spring为**表述层**开发提供的一整套完备的解决方案，封装的就是servlet。

三层架构，是指的表现层、业务逻辑层、数据访问层，表述层表示前台页面和后台servlet

### 1.3 SpringMVC特点

- Spring 家族原生产品，与 IOC 容器等基础设施无缝对接
- 基于原生的Servlet，通过了功能强大的前端控制器DispatcherServlet，对请求和响应进行统一处理
- 表述层各细分领域需要解决的问题全方位覆盖，提供全面解决方案
	代码清新简洁，大幅度提升开发效率
- 内部组件化程度高，可插拔式组件即插即用，想要什么功能配置相应组件即可
- 性能卓著，尤其适合现代大型、超大型互联网项目要求

## 2.RequestMapping注解

### 2.1 标识的位置

@RequestMapping标识一个类：设置映射请求的请求路径的初始信息

@RequestMapping标识一个方法：设置映射请求请求路径的具体信息

即，类上的路径加上方法上的路径

### 2.2 values属性

作用：通过请求的请求路径匹配请求

value属性是数组类型，即当前浏览器所发送请求的路径匹配value属性中的任何一个值，则当前请求就会被这个控制器方法进行处理

```
    @RequestMapping(value = {"/hello","/abc"})
    public String hello(){
        return "success";
    }
```



### 2.3 method属性

作用：通过请求的请求方式匹配请求

method属性是RequestMethod类型的数组，即若当前浏览器所发送请求的请求方式匹配method属性数组中的任何一种请求方式，则当前请求就会被注解所标识的方法进行处理

若浏览器所发送的请求的路径和value属性匹配，但是请求方式不匹配，则页面报错：HTTP状态 405 - 方法不允许

    @RequestMapping(
            value = {"/hello","/abc"},
            method = {RequestMethod.POST,RequestMethod.GET}
            )
    public String hello(){
        return "success";
    }

如果不指定method属性，**那就可以匹配任意类型的请求**

### 2.4 params属性

- 作用：通过请求的请求参数匹配请求，即浏览器发送的请求的请求参数必须满足params属性的设置
* 可以使用四种表达式：
* "param"：表示当前所匹配请求的请求参数中必须携带param参数，不管他的值是啥
* "!param"：表示当前所匹配请求的请求参数中一定不能携带param参数
* "param=value"：表示当前所匹配请求的请求参数中必须携带param参数且值必须为value
- "param!=value"：表示当前所匹配请求的请求参数中可以不携带param参数，若携带，值一定不等于value

### 2.5 headers属性

- 作用：通过请求的请求头匹配请求，即浏览器发送的请求的请求头必须满足headers属性的设置
* "header"：要求请求映射所匹配的请求必须携带header请求头信息
* "!header"：要求请求映射所匹配的请求必须不能携带header请求头信息
* "header=value"：要求请求映射所匹配的请求必须携带header请求头信息且header=value
* "header!=value"：要求请求映射所匹配的请求必须携带header请求头信息且header!=value
* 注意：若当前请求满足@RequestMapping注解的value和method属性，但是不满足headers属性，此时页面显示404错误，即资源未找到

### 2.6 SpringMVC支持ant风格的路径

在@RequestMapping注解的value属性中设置一些特殊字符
?：任意的单个字符(不包括?和/)
*：表示0个或多个任意字符(不包括?和/)
**：表示任意层数的任意目录，注意使用方式只能将`**` 写在双斜线中，前后不能有任何的其他字符

### 2.7 使用路径中的占位符

对比：

- 传统：/deleteUser?id=1
- rest: /deleteUser/1

使用：

需要在@RequestMapping注解的value属性中所设置的路径中，使用{xxx}的方式表示路径中的数据

再通过@PathVariable注解，将占位符的值和控制器方法的形参进行绑定

```
@RequestMapping("/test/rest/{id}/{username}")
public String testRest(@PathVariable(value = "id") Integer id,@PathVariable(value = "username")String username){

    System.out.println("id:"+id+",username:"+username);
    return "success";
}
```



## 3.SpringMVC获取请求参数

## 4.域对象共享数据

## 5.SpringMVC视图

## 6.RESTful

## 7.SpringMVC处理ajax请求

## 8.文件上传和下载

## 9.拦截器

## 10.异常处理器

## 11.注解配置SpringMVC

## 12.SpringMVC执行流程

