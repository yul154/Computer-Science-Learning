# Generics
> A generic class or interface that is parameterized over types.

```
class name<T1,T2, ..., Tn>{/*...*/}
```

## Type Parameter Naming Conventions
```
E - Element (used extensively by the Java Collections Framework)
K - Key
N - Number
T - Type
V - Value
S,U,V etc. - 2nd, 3rd, 4th types
```

## Bounded Type Parameters
>  restrict the kinds of types that are allowed to be passed to a type parameter. 

* To declare a bounded type parameter, list the type parameter's name, followed by the extends keyword, followed by its upper bound.

```
public static <T extends Comparable<T>> T maximum(T x, T y, T z)
```

## Invoking and Instantiating a Generic Type

* Enable replace the type arguments required to invoke the constructor of a generic class with an empty set of type arguments (<>) 
```
Box<Integer> integerBox = new Box<>();
```
----
# Serialization
> Encoding of objects and the objects reachable from them, into a stream of bytes.
* After a serialized object has been written into a file, it can be read from the file and deserialized that is
* the entire process is JVM independent, meaning an object can be serialized on one platform and deserialized on an entirely different platform.

* Classes `ObjectInputStream` and `ObjectOutputStream` are high-level streams that contain the methods for serializing and deserializing an object.
```
public final void writeObject(Object x) throws IOException// Serializes an Object and sends it to the output stream
public final Object readObject() throws IOException, ClassNotFoundException
```
### Conditions of serialization
1. The class must implement the java.io.Serializable interface.
2. All of the fields in the class must be serializable. If a field is not serializable, it must be marked transient.

## Serializing an Object

```
FileOutputStream fileOut =
new FileOutputStream("/tmp/employee.ser"); 
ObjectOutputStream out = new ObjectOutputStream(fileOut);
out.writeObject(e);
out.close();
```

```
FileInputStream fileIn = new FileInputStream("/tmp/employee.ser"); 
ObjectInputStream in = new ObjectInputStream(fileIn);
e = (Employee) in.readObject();
in.close();
fileIn.close();
```
---
# Sending E-mail

prerequisites: JavaMail API and Java Activation Framework (JAF) 

* Example
```
public static void main(String [] args) {
      // Recipient's email ID needs to be mentioned. 
      String to = "abcd@gmail.com";

      // Sender's email ID needs to be mentioned 
      String from = "web@gmail.com";

      // Assuming you are sending email from localhost 
      String host = "localhost";

      // Get system properties
      Properties properties = System.getProperties();

      // Setup mail server 
      properties.setProperty("mail.smtp.host", host);

      // Get the default Session object.
      Session session = Session.getDefaultInstance(properties);

      try{
          // Create a default MimeMessage object. 
          MimeMessage message = new MimeMessage(session);
          
          // Set From: header field of the header. 
          message.setFrom(new InternetAddress(from));
          
          // Set To: header field of the header. 
          message.addRecipient(Message.RecipientType.TO, new InternetAddress(to));
          
          // Set Subject: header field 
          message.setSubject("This is the Subject Line!");
          
          // Now set the actual message 
          message.setText("This is actual message");
          
          // Send message
          Transport.send(message);
         
         System.out.println("Sent message successfully....");
      }catch (MessagingException mex) { 
           mex.printStackTrace();
      } 
   }

```
