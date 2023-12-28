# Spring Framework Notes

[TOC]







入门案例开发步骤：

1. 引入spring依赖-pom.xml 
2. 创建类，定义属性和方法-User.java
3. 按照Spring要求创建配置文件-bean.java
4. Spring配置文件配置类信息-bean.java
5. 测试



#### 使用反射创建对象

1. 加载bean.xml配置文件
2. 解析xml
3. 获取bean id 和 class 属性值
4. 使用反射根据类全路径创建对象

```java
//        获取Class对象
        Class c = Class.forName("com.focus.spring6.User");
//        创建对象
        User o = (User) c.newInstance();
//        User o = c.getDeclaredConstructor().newInstance();
        o.test();
```

创建的对象放在哪：

```java
	/** Map of bean definition objects, keyed by bean name. */
	private final Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<>(256);	
```

Key:String 唯一标识 默认是类名小写

Value:BeanDefinition 类的定义，描述信息





