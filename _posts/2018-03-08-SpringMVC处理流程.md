

```mermaid

graph LR;
subgraph Spring MVC
subgraph Front Controller
DispatcherServlet   
end
HandlerMapping((HandlerMapping))
ModelMap((ModelMap))
style HandlerMapping fill:#ccf,stroke:#f66,stroke-width:2px,stroke-dasharray: 5, 5
style ModelMap fill:#ccf,stroke:#f66,stroke-width:2px,stroke-dasharray: 5, 5

Client --1.Http request--> DispatcherServlet
DispatcherServlet--2.which handler?-->HandlerMapping
HandlerMapping-.3.Handler.->DispatcherServlet
DispatcherServlet--4.handler-->HandlerAdapter
HandlerAdapter--4.1-->Handler
Handler-.4.2.which model?.->ModelMap
ModelMap-.4.3.model&view.->Handler
Handler-.4.4.model&view.->HandlerAdapter
HandlerAdapter-.5.model&view.->DispatcherServlet
DispatcherServlet--6.model--> ViewResolver
ViewResolver-.7.view.-> DispatcherServlet
DispatcherServlet--8.model--> View
View-.9.渲染.-> DispatcherServlet
DispatcherServlet-.10.return control.-> Client
end

```

## 处理流程：
### 1、HTTP请求-->DispatcherServlet
用户发送HTTP请求-->DispatcherServlet，DispatcherServlet作为统一访问点，进行全局的流程控制；

### 2、DispatcherServlet-->HandlerMapping
DispatcherServlet收到请求后到HandlerMapping中查询当前请求对应的处理器（Handler），HandlerMapping中可以查询到HTTP请求和处理函数间的mapping关系。HandlerMapping 查询到的信息以 HandlerExecutionChain 对象（Handler 处理器（Controller）对象 + 多个 HandlerInterceptor 拦截器）的形式返回给DispatcherServlet；
<!--more-->
>HandlerInterceptor接口给我们提供了3个方法：
>（1）preHandle: 在执行controller处理之前执行，返回值为boolean ,返回值为true时接着执行postHandle和afterCompletion，如果我们返回false则中断执行;
>（2）postHandle:在执行controller的处理后，在ModelAndView处理前执行;
>（3）afterCompletion ：在DispatchServlet执行完ModelAndView之后执行;


### 3、DispatcherServlet-->HandlerAdapter
DispatcherServlet将得到的Handler告知HandlerAdapter，HandlerAdapter再根据请求去定位请求的具体处理方法是哪一个。HandlerAdapter 将会把处理器包装为适配器，从而支持多种类型的处理器，即适配器设计模式的应用，从而很容易支持很多类型的处理器；

>1.DispatcherServlte会根据配置文件信息注册HandlerAdapter，如果在配置文件中没有配置，那么 DispatcherServlte会获取HandlerAdapter的默认配置，如果是读>取默认配置的话，DispatcherServlte会读取 DispatcherServlte.properties文件,该文件中配置了三种 HandlerAdapter：HttpRequestHandlerAdapter，>SimpleControllerHandlerAdapter和 AnnotationMethodHandlerAdapter。DispatcherServlte会将这三个HandlerAdapter对象存储到 它的handlerAdapters这个  >集合属性中，这样就完成了HandlerAdapter的注册。
>
>2.DispatcherServlte会根据handlerMapping传过来的controller与已经注册好了的HandlerAdapter 一一匹配，看哪一种HandlerAdapter是支持该controller类型  >的，如果找到了其中一种HandlerAdapter是支持传过来的 controller类型，那么该HandlerAdapter会调用自己的handle方法，handle方法运用Java的 反射机制执行>controller的具体方法来获得ModelAndView,例如SimpleControllerHandlerAdapter是支持 实现了controller接口的控制器，如果自己写的控制器实现了controller >接口，那么 SimpleControllerHandlerAdapter就会去执行自己写控制器中的具体方法来完成请求。

### 4、HandlerAdapter-->Handler
HandlerAdapter-->处理器功能处理方法的调用，HandlerAdapter 将会根据适配的结果调用真正的处理器的功能处理方法，完成功能处理；并返回一个ModelAndView 对象（包含模型数据、逻辑视图名）；

### 5、DispatcherServlet-->ViewResolver
DispatcherServlet将得到的ModelAndView告知ViewResolver， ViewResolver 将把逻辑视图名解析为具体的 View；

>ViewResolver的主要作用是把一个逻辑上的视图名称解析为一个真正的视图，通过这种策略模式，很容易更换其他视图技术。


### 6、View-->渲染  
View-->渲染，View 会根据传进来的 Model 模型数据进行渲染，此处的 Model 实际是一个 Map 数据结构，因此很容易支持其他视图技术；

>简单说一下render方法的最终实现机制
>
>（1）model是一个Map结构，其实就是ModelAndView中map，存放了我们返回给请求的所有结果值
>
>（2）request和response当然就是请求和返回了
>
>render中做的操作就是将model中的值全部存放到request和response中，这样就完成了请求的处理操作，最终就是返回response请求。


### 7、渲染信息-->DispatcherServlet
将渲染的信息返回给 DispatcherServlet，由 DispatcherServlet 返回response给用户。

## 开发步骤

### 1、  DispatcherServlet 在 web.xml 中的部署描述
DispatcherServlet拦截到 Spring Web MVC 的请求

### 2、  HandlerMapping 的配置
将请求映射到处理器

### 3、  HandlerAdapter 的配置
支持多种类型的处理器

### 4、  ViewResolver 的配置
将逻辑视图名解析为具体视图技术

### 5、  处理器（页面控制器）的配置
进行功能处理
