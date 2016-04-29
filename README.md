# serialize
序列化的含义：<br/>
<pre>
Serialization is the conversion of an object to a series of bytes, 
so that the object can be easily saved to persistent storage or streamed across a communication link.
The byte stream can then be deserialized - converted into a replica of the original object.
</pre>
换句话说，序列化就是将，对象转换成一系列的字节，方便数据在JNM挂掉之后，依然可以被保存<br/>
<pre>
public class Employee implemens java.io.Serializable
{
public String name;
public String address;
public transient int SSN;
public int number;
public void mailCheck(){
System.out.println("Mailing to check to "+name+" "+address);
}
}
</pre>
当变量前有transient标识符时，该变量不会被序列化<br/>
#############################<br/>
Serialize序列化<br/>
#############################<br/>
<pre>
import java.io.*;

public class SerializeDemo
{
   public static void main(String [] args)
   {
      Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
      
      try
      {
         FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
         System.out.printf("Serialized data is saved in /tmp/employee.ser");
      }catch(IOException i)
      {
          i.printStackTrace();
      }
   }
}
</pre>
##############################<br/>
Deserialize反序列化
##############################<br/>
<pre>
import java.io.*;
public class DeserializeDemo
{
   public static void main(String [] args)
   {
      Employee e = null;
      try
      {
         FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
      }catch(IOException i)
      {
         i.printStackTrace();
         return;
      }catch(ClassNotFoundException c)
      {
         System.out.println("Employee class not found");
         c.printStackTrace();
         return;
      }
      System.out.println("Deserialized Employee...");
      System.out.println("Name: " + e.name);
      System.out.println("Address: " + e.address);
      System.out.println("SSN: " + e.SSN);
      System.out.println("Number: " + e.number);
    }
}
</pre>
