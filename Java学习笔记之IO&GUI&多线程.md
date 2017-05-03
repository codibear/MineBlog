# IO概念
**概念理解**
即输入(input)，输出(output)，java中用流来描述输入输出的过程，也就是想流一样持续出入。  
- 入还是出事根据内存来说的
  - 读入内存就是输入(input) 
> 把数据读入到内存中执行read操作
  - 从内存中写出就是输出(output) 
> 把数据从内存中写出执行write操作

# File类
java.io中的重要类
**可以表示文件或目录**能对文件或目录进行他们属性的书写，比如说修改日期、大小、名字……需要注意的是他**不能对文件或目录进行读写操作---只有输入输出流才能修改**
### 用法
 - File("文件或目录名字")
 - File f1 = new File("aaa.txt")
 - File f2 = new File("D:\\java\\javafile.java")
> 双斜杠或  反斜杠用一个就行    D:\\java == D:/java

常用方法：isexits isFile isDirectory canRead getName getAbslotutePath具体作用请看相关的api

**list()**返回当前目录的子目录及文件所有名字**创建时必须熟String类的数组**
>下面是示例并通过for循环取出名字

- 1-1
~~~
File f1 = new File("D:\\test");
String [] fileName = f1.list(); //String类型数组
for(String s:fileName)
System.out.println(s);
~~~

**listFiles()**返回目录的子目录及文件的所有实例**创建时必须是File类的数组**
>下面是示例并通过for循环取出名字

- 1-2
~~~
File f1 = new File("D:\\test");
File [] fileName = f1.listFiles(); //File类型数组
for(String s:fileName)
System.out.println(s);
~~~

### list()&listFile接口
接口FilenameFilter*传的是文件名*/FileFilter*传的是文件*
调用的话就要实现接口重写里面的accept方法

> 示例：如果文件名字是java.txt就返回true

~~~
public class MyFile implement FilenameFilter{
	@override
	public boolean accept(File dir,String name)
	if(name.equal("java.txt")){
	return true;
	}else{
	return false;	
	}
}
~~~
> 调用：以上面的1-1为例返回名字为java.txt的文件

~~~
String [] name = fileName.list(new MyFile());
for(String s:name)
System.out.println(s);
~~~
FileFilter也是一样的道理


# 输入流输出流
- 输入流：往内存里读入
>相关的类有Reader类InputStream类及他们的子类如FileInputStream、FileReader
- 输出流：向内存外写出
>相关的类有Writer类OutputStream类及他们的子类（对应上面的）

# 字节流及字符流（8位/16位）
- 字节流对应的就是InputStream和OutputStream 8位 ->1字节
> 通常用于二进制、视频音频 如：FileInputStream
- 字符流对应的就是Reader和Writer 16位 ->2字节
> 通常用于文本 如：FileReader

# 节点流和处理流  
- 节点流 封装的数据源，如文件、字符……
> 如FileReader（File file）当我们要读取File类的文件时如上面的1-2通过FileReader来读，它把file封装了。即把数据源转换成构造器所需要的类型（封装数据源）
~~~
File f1 = new File("D:/java.txt");
FileReader fr = null;
try{
	fr = new FileReader(f1);
	itn i = fr.read();
	while(i!=-1){		//read方法规定当返回-1的时候读取结束
	System.out.println((char)i)	
	i = fr.read();
	}
    }catch(Exception e){
	e.printStackTrace();
	}finally{
	if(fr!= null)
	try{
	fr.close(); //一定要关闭否则会影响内存读取速率
	   }catch(Exception e){
	e.printStackTrace();
	}
	}
~~~
 >>FileInputStream FileReader 
- 处理流 封装的是流对象提供缓冲功能(所以前面一般是Buffered……如BufferedReader),能加快读写效率
> 类比上面的

~~~
FileReader fr = null;
BufferedReader br = null;
try{
	br = new BufferedReader(fr); //可以看到他是把FileReader进行了再封装
	String line = br.readLine()； //可以看到他读取的是字符串，而不是一个个字符了，所以速度快

// 也可以写在一起
	//BufferedReader br = new BufferedReader(new FileReader(fr));
	while(line!=null){
		System.out.println(line);
		line = br.readLine();
	   				 }
	}catch(Exception e ){
	e.printStackTrace();
						}
	finally{
		fr.close();
			}
~~~

# 字节流字符流的转换 -- 转换流

InputStreamReader(InputStream in)
OutputStreamReader(OutputStream out)

`示例`

BufferedReader br = new BufferedReader(new　InputStreamReader(System.in))；
> 从键盘中读取数据

# Sanner 简化了从控制台读取
Scanner sn = new Scanner(System.in)
通过nextLine nextString newInt()……获得相应类型的数据


# IO操作思想
1. 明确目的
 - 输入 InputStream Reader `读入`
 - 输出 OutputStream Writer `写出`
2. 操作数据类型
 - 字符流 Reader Writer
 - 字节流 In Out
3. 具体设备
	
4. 额外功能
	- 高效 利用缓冲区
	- 非高效 不利用
- 需求 -复制 从内存拿出在放进去 text-->textbackup

~~~
File f1 = new File("D:/text.txt")
File f2 = new File("D:/textbackup.txt")  

BufferedReader br = new BufferedReader(new FileReader(f1));
BufferedWriter bw = new BufferedReader(new FileWriter(f2));

String line = br.readLine(); //line相当于一个中介，把读取的数据存到line，然后把line传递给Write
while(line!=null)
{
	bw.writeline(line+'\n');
	line = br.readLine();
	bw.flush();  // 保证已经操作成功
	bw.close();
} 
~~~