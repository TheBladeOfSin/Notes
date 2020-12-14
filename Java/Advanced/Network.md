## 网络编程

### 概述  

> - 网络通讯：
>   在计算机领域中实现计算机与计算机之间的数据通信一种操作现象，完成数据交互处理。<font color=red>**所有信息传输都必须遵循网络协议**</font>，在网路中存在很多不同的协议。
>
> - 互联网：
>   目前计算机领域中管理和传输数据的一种载体，在该邻域中都是以计算机为基础，实现数据的交互操作，互联网是一个无形的网络每个计算机在网络中都会存在一个固定的地址，通过地址获取到计算机所在位置，并且在指定的地址上才能完成与计算机中应用软件的交互。
>   互联网从诞生到至今经过了两次变更，从pc方式发展到现在的移动设备的方式，所以现在互联网（pc）就包含了移动互联网（手机）模式。
>
> - 软件模式：
>   **C/S模式**：客户端/服务器模式
>   **B/S模式**：浏览器/服务器模式
### 划分点

* 网络协议
* Java网络编程
* 网络爬虫

> * #### **网络协议**
>
> > 互联网中网络协议包含很多种，例如TCP协议、IP协议、FTP协议、UDP协议、HTTP协议
> >
> > 为了互联网更好的管理计算机，推出了一个协议族：**TCP/IP协议族** 
> >
> > **<font color=yellow>TCP/IP协议：传输控制协议/网络协议</font>** 
> > 分层：
> >
> >
> > 1. 应用层----负责处理特定数据信息的应用程序（ftp、DNS、http）
> > 2. 传输层----对应用层处理网络连接中计算机之间的数据连接（TCP、UDP）
> > 3. 网络层----处理网络中流动的数据包 （IP协议）
> > 4. 数据链路层----处理连接网络终端的硬件部分（如：网卡）
> >
> > <font color=yellow>**http协议：**</font> 超文本传输协议，<font color=green>是目前互联网中最常见的一种协议类型</font> 
> >
> > 该协议是基于TCP/IP协议而来，实现了互联网中服务器数据请求和响应的协议控制，从诞生至今版本没有太大变化，目前都使用1.1版本进行协议约束，http协议为了提高互联网数据安全性产生出了一种<font color=yellow>http加密版本</font>的协议方式称之为：<font color=yellow>https</font> 。
> >
> > **Java网络通讯方式**：
> > 基于两种方式操作：TCP/IP方式、UDP方式
> > TCP/IP：传输控制/网际协议
> > UDP：数据报协议	<font color=green>--通过网络数据传输实现应用程序的数据抓取，将数据传输到网路</font> 
> > UDP信息包标题很短，只有8字节，而TCP/IP有20字节
> >
> > 区别：
> > 1. TCP建立在连接基础上，而UDP无连接。
> > 2. TCP对资源需求比较，UDP需求较少。
> > 3. TCP传输方式以流为基础，而UDP以数据包方式为基础
> > 4. TCP在传输中需要确保数据的有效性和正确性，而UDP会产生数据包丢失。
> > 5. TCP在传输时确保数据按照顺序传输，而UDP不确定。
> > 
> > HTTP协议:
> > API：URL、HttpURLConnection
> > URI:统一资源标识符 -->网络中的资源信息(包含URL)
> > URL:统一资源定位符 -->网络中的资源路径
>
> ---
>
>
> * #### **Java网络编程** 
> > java.net包	--网络通讯包
> >
> > API：
> > - InetAddress
> > Java中网络地址对象，用于获取计算机中网络地址的一种对象
> > - Socket
> > Java网络编程又称Socket编程
> > 因为TCP/IP协议方式的程序都是基于C/S模式的应用程序，在完成网络编程时必须建立在连接的基础上，协议方式属于一对多的网络通信TCP/IP通讯
> >
> > InetAddress类的实例对象包含以数字形式保存的IP地址，同时还可能包含主机名，InetAddress类提供了将主机名解析为IP地址（或反之）的方法。<font color=red>InetAddress没有构造函数。</font> 
> >
> > ``` java
> > public class InetAddressDemo {
> > 	public static void main(String[] args) {
> > 		try {
> > 			//获取地址对象
> > 			InetAddress ip=InetAddress.getLocalHost();
> > 			System.out.println("本机IP地址："+ip.getHostAddress());
> > 			System.out.println("本机机器名："+ip.getHostName());
> > 			//创建一个获取远程计算机地址对象
> > 			InetAddress ip1=InetAddress.getByName("118.249.100.91");
> > 			System.out.println(ip1.getHostAddress()+"--"+ip1.getHostName());
> > 		} catch (UnknownHostException e) {
> > 			e.printStackTrace();
> >         }
> > 	}
> > }
> > ```
> >
> > 
> >
> > 基于TCP/IP协议方式实现Socket编程
> > 通过一对一的方式将客户端信息发送给服务器，服务器能通过多个连接客户端进行客户端的群发操作。
> >
> > C/S模式实现即时通讯
> > 即时通讯需要服务器及时响应客户端发送消息，并且能及时地将信息发送给所有连接的客户端。
> > 打印流：
> > 	1.基于TCP/IP协议 -PrintStream
> > 	2.基于HTTP协议 -PrintWriter 
> >
> > 通过Socket实现的简单聊天群：
> > 服务端：
> >
> > ``` java
> > public class SocketServer {
> > 	public static void main(String[] args) {
> > 		//客户端连接集合
> > 		List<Socket> list=new ArrayList<Socket>();
> > 		try {
> > 			//服务器
> > 			ServerSocket server=new ServerSocket(8888);
> > 			while(true) {
> > 				//将客户端连接存储到集合中
> > 				Socket client=server.accept();
> > 				synchronized(list) {//存储客户端连接至集合存在同步问题
> > 					list.add(client);
> > 				}
> > 				//调用服务器读写线程操作
> > 				new ServerThread(client,list).start();
> > 			}
> > 		} catch (IOException e) {
> > 			e.printStackTrace();
> > 		}
> > 	}
> > }
> > ```
> >
> > 服务端线程：
> >
> > ``` java
> > public class ServerThread extends Thread {
> > 	//客户端对象
> > 	Socket client;
> > 	//定义客户端集合对象
> > 	List<Socket> list;
> > 	
> > 	public ServerThread(Socket client,List<Socket> list) {
> > 		this.client=client;
> > 		this.list=list;
> > 	}
> > 	
> > 	public void run() {
> > 		//获取当前连接的客户端信息
> > 		InetAddress ip=client.getInetAddress();
> > 		System.out.println(ip.getHostAddress()+"上线了");
> > 		try {
> > 			//读取客户端发送消息
> > 			BufferedReader br=new BufferedReader(new InputStreamReader(client.getInputStream()));
> > 			String data="";
> > 			//读取信息
> > 			while((data=br.readLine())!=null) {
> > 				String msg="IP:"+ip.getHostAddress()+",Content:"+data;
> > 				//发送消息给所有客户端
> > 				sendAll(msg);
> > 			}
> > 		} catch (IOException e) {
> > 			//如果客户端信息读取产生异常表示客户端断开
> > 			System.out.println(ip.getHostAddress()+"下线");
> > 			synchronized(list){
> > 				list.remove(client);
> > 			}
> > 		}
> > 	}
> >     
> > 	//同步群发送信息方法
> > 	public synchronized void sendAll(String msg) {
> > 		//循环遍历所有连接服务器的客户端连接对象
> > 		for(Socket c:list) {
> > 			//排除当前客户端连接对象
> > 			if(c!=client) {
> > 				try {
> > 					//通过打印字节流进行信息发送
> > 					PrintStream print=new PrintStream(c.getOutputStream());
> > 					//--println方法自带刷新功能
> > 					print.println(msg);
> > 				} catch (IOException e) {
> > 					e.printStackTrace();
> > 				}
> > 			}
> > 		}
> > 	}
> > }
> > ```
> >
> > 客户端：
> >
> > ``` java
> > public class SocketClient {
> > 	public static void main(String[] args) {
> > 		try {
> > 			//客户端连接服务端
> > 			Socket client=new Socket("127.0.0.1",8888);
> > 			//向服务端发送信息
> > 			new ClientSendThread(client).start();
> > 			new ClientRecevieThread(client).start();
> > 		} catch (UnknownHostException e) {
> > 			e.printStackTrace();
> > 		} catch (IOException e) {
> > 			e.printStackTrace();
> > 		}
> > 		
> > 	}
> > }
> > ```
> >
> > 客户端发送消息线程：
> >
> > ``` java
> > public class ClientRecevieThread extends Thread {
> > 	//客户端连接对象
> > 	Socket client;
> > 	public ClientRecevieThread(Socket client) {
> > 		this.client=client;
> > 	}
> > 	
> > 	@Override
> > 	public void run() {
> > 		try {
> > 			//通过字符缓冲区进行数据读取
> > 			BufferedReader br=new BufferedReader(new InputStreamReader(client.getInputStream()));
> > 			String data="";
> > 			while((data=br.readLine())!=null) {
> > 				System.out.println(data);
> > 			}
> > 		} catch (IOException e) {
> > 			e.printStackTrace();
> > 		}
> > 	}
> > }
> > ```
> >
> > 客户端接收消息线程：
> >
> > ``` java
> > public class ClientSendThread extends Thread {
> > 	//客户端连接对象
> > 	Socket client;
> > 	public ClientSendThread(Socket client) {
> > 		this.client=client;
> > 	}
> > 	
> > 	@Override
> > 	public void run() {
> > 		//定义控制台输入
> > 		Scanner in=new Scanner(System.in);
> > 		while(true) {
> > 			System.out.println("请输入信息：");
> > 			String out=in.next();
> > 			try {
> > 				//通过打印字节流进行信息发送
> > 				PrintStream ps=new PrintStream(client.getOutputStream());
> > 				ps.println(out);
> > 			} catch (IOException e) {
> > 				System.out.println("服务器已断开");
> > 				System.exit(0);
> > 			}
> > 		}
> > 	}
> > }
> > ```
> >
> > ---
> >
> > HTTP协议API
> > 			API：URL、HttpURLConnection
> > 			URI:统一资源标识符 -->网络中的资源信息(包含了URL的)
> > 			URL:统一资源定位符 -->网络中的资源路径
> >
> > 利用http将某网站上的内容读写到test.html文件中：
> >
> > ``` java
> > public class HttpDemo {
> > 	public static void main(String[] args) {
> > 		FileWriter fw=null;
> > 		BufferedReader br=null;
> > 		try {
> > 			//创建资源路径对象	--https的加密网站无法爬取
> > 			URL url=new URL("http://www.java1234.com/");
> > 			//通过资源路径对象开启连接并获取连接对象
> > 			HttpURLConnection http=(HttpURLConnection)url.openConnection();
> > 			//定义文件字符流存储数据
> > 			br=new BufferedReader(new InputStreamReader(http.getInputStream()));
> > 			fw=new FileWriter(new File("test.html"));
> > 			String str="";
> > 			//边读边写
> > 			while((str=br.readLine())!=null) {
> > 				fw.write(str);
> > 			}
> > 		} catch (MalformedURLException e) {
> > 			e.printStackTrace();
> > 		} catch (IOException e) {
> > 			e.printStackTrace();
> > 		}finally {
> > 			try {
> > 				fw.close();
> > 				br.close();
> > 			} catch (IOException e) {
> > 				e.printStackTrace();
> > 			}
> > 		}
> > 	}
> > }
> > ```
>
> ---
>
> **网络爬虫** 
>
> > 通过指定的标签class进行对应数据的爬取行为就称之为网络爬虫。
> >
> > jsoupAPI是Java网络爬虫的API，可以通过标签class数据进行节点爬取。



<font color=red></font>
<font color=yellow></font>
<font color=green></font>