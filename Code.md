Exp 3:-
Addclass Code:- 


public class Addclass {
	public int add(int a, int b) {
		return a+b;
	}

}


Exp 4:-

IHello code:- 

import java.rmi.*;
public interface IHello extends Remote{
	public String message() throws RemoteException;

}

HelloServer Code:-

import java.rmi.*;
public class HelloServer {
	private static final String host = "localhost";
	
	public static void main(String[] args) throws Exception {
		
		HelloImpl temp = new HelloImpl();
		
		
		String rmiObjectName = "rmi://" + host + "/Hello";
		
		Naming.rebind(rmiObjectName, temp);
		
		System.out.println("Binding complete....\n");
	}

}


HelloImpl Code:- 

import java.rmi.*;
import java.rmi.server.*;
public class HelloImpl extends UnicastRemoteObject
		implements IHello{
	public HelloImpl() throws RemoteException {
		//There is no action need    In this moment.
	}
	public String message() throws RemoteException{
		return ("Hello");
	}
}


HelloClient Code:-

import java.rmi.ConnectException;
import java.rmi.Naming;
	
public class HelloClient
{
	private static final String host = "localhost";
	
	public static void main(String[] args)
	{
		try
		{
			//We obtain a reference to the object from the registry and next,
			//it will be typecasted into the most appropriate type.
			IHello greeting_message = (IHello) Naming.lookup("rmi://" 
					+ host + "/Hello");
			
			//Next, we will use the above reference to involve the remote
			//object method.
			System.out.println("Message received: " + 
					greeting_message.message());
		}
		catch (ConnectException conEx)
		{
			System.out.println("Unable to connect to server!");
			System.exit(1);
		}

		catch (Exception ex)
		{
			ex.printStackTrace();
			System.exit(1);
		}
}
}

 
*Start rmiregistry*

Exp 5:-

Client:
package middleware;

public class Client{
	public static void main(String [] args) 
	{
		Server i= new Server();
		System.out.println(i.add(12,13));
		System.out.println(i.sub(12,12));
	}

}

Server:- 

package middleware;

public class Server {
	public int add(int a, int b) {
		return a+b;
	}
	public int sub(int a, int b) {
		return a-b;
	}
}

interfaceCalculator:- 

package middleware;

public class interfaceCalculator {
	public int add(int a, int b);
	public int sub(int a, int b);
}



Exp 6:-
 
Sender code:

package wrapper;

import java.net.*;
import java.util.*;
public class Sender {
public static void main(String[] args) throws Exception{
	Scanner scn=new Scanner(System.in);
	System.out.println("Enter your Message: ");
	String str=scn.nextLine();
	DatagramSocket ds=new DatagramSocket();
	InetAddress ip=InetAddress.getByName("127.0.0.1");
	DatagramPacket dp=new
	DatagramPacket(str.getBytes(),str.length(), ip, 3000);
	ds.send(dp);
	ds.close();
	System.out.println("Message has been sent to Receiver Class Please Check: "+str);
	}
}


Receiver Code:-

package wrapper;

import java.net.*;
public class Receiver {

	public static void main(String[] args) throws Exception{
	System.out.println("Waiting for sender to send message");
	DatagramSocket ds=new DatagramSocket(3000);
	byte[] buf=new byte[1024]; 
	DatagramPacket dp=new DatagramPacket(buf,1024); 
	ds.receive(dp); 
	String str=new String(dp.getData(),0,dp.getLength()); 
	System.out.print(str); 
	ds.close();
	System.out.println("Message received Successfully..");
	}
}
