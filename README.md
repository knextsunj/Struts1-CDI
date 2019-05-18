struts-cdi
==========
CDI support for Apache Struts 1.x

This is a modified fork of https://github.com/reegnz/struts-cdi to use CDI in Java EE 7 projects with Struts 1.x as the web 
framework. It is intended to support the struts 1.3.x versions released from the following fork of apache struts 1:

https://github.com/albfernandez/struts1

What is struts-cdi
-------------
This is a java library for Struts 1.x that enables @Inject style dependency injection (DI) and the 
usage of contextual instances supported by the CDI specification.

So basically it is **CDI support for struts actions**. On Struts actions you can use the various 
styles of DI (constructor, setter and field), interceptors, decorators and events.

The library is compatible with struts versions 1.2.9, 1.3.10

How to use it
----------------
**struts < 1.3**

use struts.cdi.CdiRequestProcessor or struts.cdi.TilesCdiRequestProcessor.

You can do this by adding the following to your struts-config.xml:

        <controller nocache="true"processorClass="struts.cdi.CdiRequestProcessor">
        </controller>
        
**struts >= 1.3**

You can still use the previously described request processors. Struts 1.3 introduced the
chain of responsibility pattern, so there is a simpler alternative.

In web.xml add this init parameter to the struts servlet:

        <init-param>
            <param-name>chainConfig</param-name>
            <param-value>struts/cdi/chain-config.xml</param-value>
        </init-param>
        
If you already use a custom chain configuration, add the following command to your custom 
chain-config.xml configuration instead replacing the CreateAction command:
        
        <command className="struts.cdi.CreateCdiAction"/>

The Action creation only works, if a CDI BeanManager is available at either of the following 
JNDI locations:

        java:comp/BeanManager 
        java:comp/env/BeanManager
         
This could be provided by your application (by bundling a CDI implementation with your app) 
or by the container that the application is deployed to.

Will ActionForms be supported as well?
--------------------------------------
There is no support currently for Action Forms


