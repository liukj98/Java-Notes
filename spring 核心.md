## 理解 Spring

> **前置知识：**
>
> 1. 在 Java 领域，我们常说的 **SSH** 是指 Struct2 + Spring + Hibernate
> 2. 在 Java 领域，我们常说的 **SSM** 是指 SpringMVC + Spring + Mybatis
> 3. 其中 SSM 中的 SpringMVC 对应 SSH 中的 Struct2、Spring 对应 Spring、Mybatis 对应 Hibernate。目前我们只需要学习 SSM 即可
>
> **POJO（Plain Old Java Object）**：简单的 java 对象

Spring 是一个框架，该框架的核心技术有两个：**IOC** 和 **AOP**

1. **IOC（Inversion Of Control）**：**控制反转**。将对象的创建、对象与对象之间的依赖关系都交由 Spring 进行管理，开发人员无需关注。控制反转是一种设计思想，在 Spring 中实现这种思想的方式是 **DI（Dependency Injection）**，底层使用的是**反射机制**
2. **AOP（Aspect Oriented Programming）**：**面向切面编程**

由于所有对象交由 Spring 管理，所以 Spring 又称之为**容器**

## IDEA 搭建 Spring 项目步骤

### 1、创建一个空项目

### 2、在这个空项目中创建一个模块（module）

- 该模块是基于 `maven` 项目构建

- 由于项目是 Spring 项目，所以需要在 maven 配置文件（pom.xml）中加入 Spring 相关依赖。目前只需加入 `spring-context` 依赖即可，因为 `spring-context` 模块依赖于另外四个模块：`spring-aop`、`spring-beans`、`spring-core`、`spring-expression`。maven 会根据依赖关系自动下载相关的依赖

  > 注意⚠️：一个项目中可以创建多个模块，由于目前处于学习阶段，所以在该项目下暂时创建一个模块，模块名为 spring-ioc。之后会学习 Spring 的另一个核心概念 AOP，到时在该项目下又建一个模块，模块名为 spring-aop

### 3、创建 Spring 配置文件并进行相关配置

- **在项目的 src/main/resources 目录下创建一个 Spring 配置文件，文件名为 beans.xml**。注意：Spring 配置文件的名称书写无要求

- Spring 配置文件中的配置很简单，主要是 bean 元素的相关配置

## DI（依赖注入）

在 Spring 配置文件中，当你添加了 bean 元素 `<bean id="hello" class="org.example.Hello"/>`，在 Spring 底层会你做这样一层处理：`org.example.Hello hello = new org.example.Hello();` ，通过无参构造函数创建对象，实际是通过**反射机制**来创建对象的。bean 元素 class 属性的值为 `全限定类名` ，在这里就是 `org.example.Hello`；其中 id 属性的值为根据 `全限定类名` 创建好的对象名，在这里就是 `hello`。创建好对象后会通过 `springMap.put(id值, 对象)` 把对象放入到 map 中，例如：`springMap.put("hello", new org.example.Hello())`

### 依赖

bean 对象的创建依赖于容器（Spring）

### 注入

bean 对象中的所有属性，由容器注入，在 Spring 中注入的方式有：**基于构造函数的依赖注入**、**基于 setter 的依赖注入**、其他扩展方式注入

#### 构造函数注入

**通过 constructor-arg 标签进行构造函数注入**。之所以叫做「构造函数注入」是因为 Spring 在解析 xml 文件内容时，看到 constructor-arg 会调用对应类的构造函数来创建对象

```xml
<bean id="cat" class="org.example.Cat">
  <!-- 通过 name 进行构造函数注入 -->
  <!--        <constructor-arg name="name" value="小猫咪" />-->
  <!--        <constructor-arg name="age" value="12" />-->
  <!--        <constructor-arg name="school" ref="school" />-->
  <!--        <constructor-arg index="0" value="小猫咪" />-->
  <!--        <constructor-arg index="1" value="12" />-->
  <!--        <constructor-arg index="2" ref="school" />-->
  <constructor-arg value="小猫咪" />
  <constructor-arg value="12" />
  <constructor-arg ref="school" />
</bean>
```

#### set 注入（重点）

**通过 property 标签进行 set 注入**。之所以叫做「set 注入」是因为 Spring 在解析 xml 文件内容时，看到 property 标签会调用对应类的 setter 方法对属性进行设置。比如下面的配置：`<property name="desc" value="这是一所好大学，期待你的加入"/>` ，Spring 在创建对象后会调用对象的 `setDesc` 方法，并将 `"这是一所好大学，期待你的加入"` 作为该方法的参数传递进行，而这个方法名来自于 `set 拼接上 property 标签的 name 属性值首字母大写`

```xml
<bean id="school" class="org.example.School">
  <!-- 通过 property 进行 set 注入 -->
  <property name="name" value="Hunan University"/>
  <property name="desc" value="这是一所好大学，期待你的加入"/>
</bean>

<bean id="student" class="org.example.Student">
  <!-- 通过 property 进行 set 注入 -->
  <property name="name" value="Lkj"/>
  <property name="age" value="18"/>
  <property name="school" ref="school"/>
</bean>
```

#### 其他扩展方式注入

**c 命名**

**p 命名**

### Bean 的作用域

**单例模式（singleton）**

**原型模式（prototype）**

## Bean 的自动装配

### 使用 byName 自动装配

### 使用 byType 自动装配

### 使用注解实现自动装配

## 使用注解进行开发

