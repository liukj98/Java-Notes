## 理解 Spring

> **前置知识：**
>
> 1. 在 Java 领域，我们常说的 **SSH** 是指 Struct2 + Spring + Hibernate
>
> 2. 在 Java 领域，我们常说的 **SSM** 是指 SpringMVC + Spring + Mybatis
> 3. 其中 SSM 中的 SpringMVC 对应 SSH 中的 Struct2、Spring 对应 Spring、Mybatis 对应 Hibernate。目前我们只需要学习 SSM 即可

Spring 是一个框架，该框架的核心技术有两个

1. **IOC（Inversion Of Control）**：**控制反转**。将对象的创建、对象与对象之间的依赖关系都交由 Spring 进行管理，开发人员无需关注。控制反转是一种设计思想，在 Spring 中实现这种思想的方式是 **DI（Dependency Injection）**，底层使用的是**反射机制**
2. **AOP（Aspect Oriented Programming）**：**面向切面编程**

由于所有对象交由 Spring 管理，所以 Spring 又称之为**容器**

### DI（依赖注入）

1. 依赖：bean 对象的创建依赖于容器（Spring）
2. 注入：bean 对象中的所有属性，由容器注入
   1. 构造函数注入
   2. **set 注入（重点）**
   3. 其他扩展方式注入

## IDEA 搭建 Spring 项目步骤

### 1、创建一个空项目

### 2、在这个空项目中创建一个模块（module）

该模块是基于 `maven` 项目构建

由于项目是 Spring 项目，所以需要在 maven 配置文件（pom.xml）中加入 Spring 相关依赖。目前只需加入 `spring-context` 依赖即可，因为 `spring-context` 模块依赖于另外四个模块：`spring-aop`、`spring-beans`、`spring-core`、`spring-expression`。maven 会根据依赖关系自动下载相关的依赖

> 注意⚠️：一个项目中可以创建多个模块，由于目前处于学习阶段，所以在该项目下暂时创建一个模块，模块名为 spring-ioc
>
> 之后会学习 Spring 的另一个核心概念 AOP，到时在该项目下又建一个模块，模块名为 spring-aop

### 3、创建 Spring 配置文件并进行相关配置

在主程序的 resources 目录下创建一个 Spring 配置文件，文件名为 beans.xml，注意：配置文件名无要求

Spring 配置文件中的配置很简单，主要是 bean 元素的相关配置