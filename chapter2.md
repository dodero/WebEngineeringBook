# Web construction frameworks

## Web Application Frameworks

In a few words, web frameworks are software frameworks used to construct web applications. In a more ellaborate fashion, [web application frameworks](http://en.wikipedia.org/wiki/Web_application_framework) provide an abstraction to deal with the HTTP issues in the communication that occurs between client-side and server-side components of a distributed wep application. To describe it more accurately, we have to explain first what is a software framework.

### What is a software framework

According to the wikipedia, 

> A software framework is an abstraction in which software providing generic functionality can be selectively changed by additional user-written code, thus providing application-specific software.

A software framework is a specific type of _library_ in which their components collaborate to form a reusable design for a specific type of software. Such components are designed by following a specific __architecture__. According to ISO/IEC/IEEE 42010,

> An architecture framework establishes a common practice for creating, interpreting, analyzing and using architecture descriptions within a particular domain of application or stakeholder community. 

According to the _Gang of Four_ (Gamma et al.), the framework provides the architectural guidelines that divide the design up in abstract components (e.g. classes and interfaces). These guidelines define the responsabilities and collaborations between such components. Developers can customize the framework components by defining subclasses and composing instances.

The primary difference between _software framework_ and _software library_ lays on where is the control of the program flow. In a library, the user-programmed components manages the flow of control and calls the library components (usually, functions or procedures) whenever needed.

![Control flow in a software library](library-controlflow.png)

On the other hand, a software framework manages the main flow of control and calls the user-programmed components that are provided by the developer by extending, subclassing o composing other components.

![Control flow in a software framework](framework-controlflow.png)

The design of a framework is based on __abstract__ classes and components and the use of __open__ interfaces. All classes, modules, functions, etc. should be open for extension, but closed for modification, according to the [Open-Closed principle](http://en.wikipedia.org/wiki/Open/closed_principle). Frameworks push for an intensive use of __design patterns__. 

#### Inversion of Control

Frameworks are heavily based on the [inversion of control](http://en.wikipedia.org/wiki/Inversion_of_control) (IoC) principle, which means that dependencies with other components must be injected, not explicitly acquired.

An example of application of the IoC principle to build a web application is described below. Here is an example of an `OrderService` component programmed in Java (i.e. a _bean_, using the Java terminology). It follows the Enterprise Java Beans (EJB) specifications:

```java
private OrderService orderService;
public void doRequest(HttpServletRequest request) {
  Order order = createOrder(request);
  OrderService orderService = getOrderService();
  orderService.createOrder(order);
}
private OrderService getOrderService() throws CreateException {
  if (orderService == null) {
    Context initial=new InitialContext();
    Context myEnv = (Context) initial.lookup("java:comp/env");
    Object ref = myEnv.lookup("ejb/OrderServiceHome");
    OrderServiceHome home = (OrderServiceHome)
         PortableRemoteObject.narrow
             (ref, OrderService.class);
    orderService = home.create();
  }
  return orderService;
}
private OrderService getOrderService() {
  OrderServiceHome home =
    ServiceLocator.locate(OrderServiceHome);
  OrderService orderService = home.create();
}
```
The following is the implementation of the same component by means of the Spring framework, which includes basic IoC facilities to inject dependencies into the `OrderService` component.

```java
private OrderService orderService;

public void doRequest(HttpServletRequest request) {
  Order order = createOrder(request);
  orderService.createOrder(order);
}

public void setOrderService(OrderService orderService) {
  this.orderService = orderService;
}
```



## Types of web frameworks

The primary characteristic of Web frameworks is that they are aimed at building web applications. That means, they provide an abstraction to deal with HTTP issues to overcome HTTP limitations for programming distributed applications. That programming abstraction is an API that provides a more comfortable way to use HTTP verbs (GET, POST, PUT, DELETE, etc.), manage user sessions, etc.

The second characteristic of Web frameworks is their architectural pattern, which is usually (or is often based on) the [Model-View-Controller](http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) (MVC) pattern. 

Early web MVC frameworks placed the entire model, view and controller logic on the server. These are known as server-side or thin client MVC frameworks. In this approach, the client sends either hyperlink requests or form input to the controller and then receives a complete and updated web page (or other document) from the view. As client technologies have matured, more modern client MVC frameworks have been created that allow the MVC components to execute partly on the client.

There are many types of software frameworks that are ready or useful to create web applications. These can be classifed as follows:

* Server-side, basic: JEE JSP/Servlets, PHP, Django
* Server-side, MVC web layer: Struts, WebWork, JSF, Tapestry, CodeIgniter, Symfony, Laravel, Django, etc.
* Persistence layer: JPA, Hibernate, iBatis, etc.
* Client-side: GWT, Facelets, Vaadin, AngularJS, Ember.js, etc.
* Generic: JEE, Spring, NodeJs
* Generative: Rails, Grails, Spring ROO, Yii, etc.

There may be other alternative classifications.

MVC frameworks can be classified as:

* Action frameworks: e.g. Struts, Rails, Grails
![Action MVC frameworks](action-mvc-framworks.png)
* User Interface (UI) component frameworks: e.g. JSF, Vaadin
![UI MVC frameworks](ui-mvc-frameworks.png)
* Hybrid frameworks: e.g. Tapestry, Wicket
![Hybrid MVC frameworks](hybrid-mvc-framworks.png)
## Web framework features

A web framework can be evaluated according to a number of features, such as:

* Programming language
* Documentation
* Speed of development
* Scalability (caching, pooling, etc.)
* Tool support (IDE, web design)
* Maintainability and durability
* Community, trends

The selection of a web framework depends on the developer's or organization's abilities, the type of application that needs to be built, the performace requirements, etc.


### Trends

Trends:

<div style="width:540px">
<a href="http://www.indeed.com/jobtrends?q=jsf%2C+ruby+rails%2C+django%2C+symfony%2C+grails%2C+spring+roo" title="jsf, ruby rails, django, symfony, grails, spring roo Job Trends">
<img width="540" height="300" src="http://www.indeed.com/trendgraph/jobgraph.png?q=jsf%2C+ruby+rails%2C+django%2C+symfony%2C+grails%2C+spring+roo" border="0" alt="jsf, ruby rails, django, symfony, grails, spring roo Job Trends graph">
</a>
</div>

Benchmarks:

[![Web framework benchmarks](techempower.png)](http://www.techempower.com/benchmarks/)

## Language-specific frameworks

### PHP frameworks

### Java frameworks

### Ruby frameworks

### Python frameworks



