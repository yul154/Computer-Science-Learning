# Applet

* An applet is a Java program that runs in a Web browser.

**Differennces betweennsn an applet and a standalone Java application**
1. An applet is a Java class that extends the java.applet.Applet class.
2. A main() method is not invoked on an applet, and an applet class will not define main().
3. Applets are designed to be embedded within an HTML page.
4. When a user views an HTML page that contains an applet, the code for the applet is downloaded to the user's machine.
5. A JVM is required to view an applet. The JVM can be either a plug-in of the Web browser or a separate runtime environment
6. The JVM on the user's machine creates an instance of the applet class and invokes various methods during the applet's lifetime.
7. Applets have strict security rules that are enforced by the Web browser
8. Other classes that the applet needs can be downloaded in a single Java Archive (JAR) file.

## Life Cycle of an Applet

1. `init`: initializationapplet. It is called after the param tags inside the applet tag have been processed.
2. `start`: This method is automatically called after the browser calls the init method.It is also called whenever the user returns to the page containing the applet after having gone off to other pages.
3. `stop`: This method is automatically called when the user moves off the page on which the applet sits
4. `destory`:This method is only called when the browser shuts down normally.
5. `paint`:Invoked immediately after the start() method, and also any time the applet needs to repaint itself in the browser.

## Applet Class

```
public class HellowWord extends Applet{

    public void patin(Graphics g){
       g.drawString("Hellow, World", 25 ,50);
    }
}
```
* Every applet is an extension of the java.applet.Applet class. 
* The base Applet class provides methods that a derived Applet class may call to obtain information and services from the browser context.
```
public String getParameter(String name);
public void resize(Dimension d);
public String getAppletInfo();
```

## Invoking an Applet
> An applet may be invoked by embedding directives in an HTML file and viewing the file through an applet viewer or Java-enabled browser.

<applet> tag is the basis for embedding an applet in an HTML file
```
<html>
<title>The Hello, World Applet</title>
<hr>
<applet code="HelloWorldApplet.class" width="320" height="120"> If your browser was Java-enabled, a "Hello, World"
message would appear here.
</applet>
<hr>
</html>
```

---
# Documentation Comments 

Javadoc: tool which comes with JDK and it is used for generating Java code documentation in HTML format from Java source code, which requires documentation in a predefined format.

<img width="454" alt="Screen Shot 2020-07-01 at 12 34 54 PM" src="https://user-images.githubusercontent.com/27160394/86274419-475db200-bb97-11ea-9534-1863b836c1fe.png">
