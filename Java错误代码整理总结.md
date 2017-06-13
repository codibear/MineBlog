##快捷键
~~~
psvm  main方法
soutv  输出
~~~

# java 错误代码经验整理
C:\app\29185\product\11.2.0\dbhome_1
### 取最大值最小值

```
float min = 0;
for(int i = 0;i<studentSop.length - 1;i++){
    if(studentSop[i].getStudentNum()< studentSop[i+1].getStudentNum()){
        min = studentSop[i].getStudentNum();
    }else {
        min = studentSop[i+1].getStudentNum();
    }
}
System.out.println("最低成绩："+min);
break;
```
错误分析
> 1.min设成了0,那么不管怎么样，如果正确了，最后也是0
> 2.用[i]与[i+1]比较，比较后，虽说这组最小值给了min，下一次循环所以一直是两个为一组比较，并不能比较出整体的最小值。
> `例：11 22 33 44 55`比较11 22 后11最小赋值给min，然后下一循环开始比较22 33此时最小值就是22 了

`正确代码示例`

```
float min = studentSop[0].getStudentNum(); //
for(int i = 0;i<studentSop.length ;i++){
    if(min > studentSop[i].getStudentNum()){
        min = studentSop[i].getStudentNum();
    }
}
System.out.println("最低成绩："+min);
```
**总结：比较大小从数组的第一个就开始，把第一个最为最开始的标准**

### 面向对象思想的重要性

题目
```
春节晚会最喜爱节目评选模拟程序
要求：
1、功能描述：春节晚会有四类节目，每类节目的类型名称及代号分别为 小品  X，  舞蹈  W，独唱   D，杂技  Z。程序操作员将每张观众的选票上所填的代号（X、W、D、或Z）循环输入电脑，输入字母E结束输入，然后将所有节目的得票情况显示出来，并显示最终获奖节目的信息。
2、具体要求如下：
（1）要求用面向对象方法，编写节目类JieMu，将节目的类型名称、代号和票数保存到类JieMu的对象中，并实现相应的getXXX 和 setXXX方法。
（2）编写主程序class OneTest（请考试学员统一使用主类名称：OneTest）
（3）输入数据之前，显示出各类节目的代号及类型名称：（提示：建立一个节目类型数组）如下图所示。
（4）循环执行接收键盘输入的节目代号，直到输入的数字为E，结束选票的输入工作，如下图所示
（5）在接收每次输入的选票后要求验证该选票是否有效，即：如果输入的数不是X，D，W，Z，E这5个字母之一，应显示出错误提示信息：此选票无效，请输入正确的节目代号！并继续等待输入。
（6）输入结束后显示所有节目的得票情况，如图所示
（7）输出最终获奖节目的相关信息，如图所示。
（8）建议用函数实现获得最终获选节目的功能（提示：以节目数组为参数，返回类型为：节目类型）
（9）从控制台接受输入数据，可以参考使用下面的代码
       （10）只要提交源代码OneTest.java 和 JieMu.java

三、参考图示：

```
![最终显示](http://i.imgur.com/w5IpaQQ.png)

我一开始的编程思想，有点像面向过程了，并没有意识到票这个对象

```
package com.icss.test.homework3;

/**
 * Created by 29185 on 2017/5/24.
 */
public class JieMu {
    private int X;
    private int W;
    private int D;
    private int Z;
    JieMu(){}
    JieMu(int X,int W,int D,int Z){
        this.X = X;
        this.W = W;
        this.D = D;
        this.Z = Z;
    }

    public int getD() {
        return D;
    }

    public int getW() {
        return W;
    }

    public int getX() {
        return X;
    }

    public int getZ() {
        return Z;
    }

    public void setD(int d) {
        D += d;
    }

    public void setW(int w) {
        W += w;
    }

    public void setX(int x) {
        X += x;
    }

    public void setZ(int z) {
        Z += z;
    }
}

```
```
package com.icss.test.homework3;

import java.util.Scanner;

/**
 * Created by 29185 on 2017/5/24.
 */
class OneTest {
    public static void main(String [] args){
        System.out.println("选举开始！节目代号及类型名称如下：\n"+"X : 小品\n"+"D ：独唱\n" +"W ：舞蹈\n" + "Z ：杂技\n");
        JieMu [] jieMus = new JieMu[4];
        JieMu jieMu1 = new JieMu();
        JieMu jieMu2 = new JieMu();
        JieMu jieMu3 = new JieMu();
        JieMu jieMu4 = new JieMu();
        boolean flag = true;
        while(flag){
            Scanner input = new Scanner(System.in);
            System.out.println("请输入您喜欢的节目代号（输入E结束）：");
            String touPiao = input.nextLine();
            switch (touPiao){
                case "X":
                    jieMu1.setX(1);
                    jieMus [0]= jieMu1;
                    break;
                case "W":
                    jieMu2.setW(1);
                    jieMus [1]= jieMu2;
                    break;
                case "D" :
                    jieMu3.setD(1);
                    jieMus [2]= jieMu3;
                    break;
                case "Z":
                    jieMu4.setZ(1);
                    jieMus [3]= jieMu4;
                    break;
                case "E":
                    flag = false;
                    break;
                    default:
                        System.out.println("此选票无效，请输入正确的节目代号！");
                        break;
            }

        }
        System.out.println("小品 ： "+jieMus[0].getX());
        System.out.println("独唱 ： "+jieMus[2].getD());
        System.out.println("舞蹈 ： "+jieMus[1].getW());
        System.out.println("杂技 ： "+jieMus[3].getZ());

       /* System.out.println("小品 ： "+jieMus[0].getX());
        System.out.println("独唱 ： "+jieMus[1].getD());
        System.out.println("舞蹈 ： "+jieMus[2].getW());
        System.out.println("杂技 ： "+jieMus[3].getZ());*/
    }

}

```
应该有面向对象思维，分析有几个对象
分析：
票---属性：
代号 、 作品名 、 票数；
票---方法：
输出信息 1. 代码+名字  2.名字+票数  3. 最多 名字+票数
票数增加
判断是否输入合法

~~~
package com.icss.test.homework3_change;

/**
 * Created by 29185 on 2017/5/25.
 */
public class JIeMu {
    private String name;
    private String id;
    private int ticket;
    JIeMu(){}
    JIeMu(String name, String id){
        this.name = name;
        this.id = id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setTicket(int ticket) {
        this.ticket = ticket;
    }

    public String getName() {
        return name;
    }

    public int getTicket() {
        return ticket;
    }

    public String getId() {
        return id;
    }
    //对票数进行+1
    public void addTicket(){
        this.ticket++;
    }
    //判断输入是否合法
    public boolean isSameCode(String code){
        return this.id.equalsIgnoreCase(code);
    }
    //  shuchu
    public void showMsg(int index){
        switch (index){
            case 1:
                System.out.println(this.id+":"+this.name);
                break;
            case 2:
                System.out.println(this.name+":"+this.ticket);
                break;
            case 3:
                System.out.println("观众最喜欢的节目是："+this.name+"获得"+this.ticket+"票");
                break;
            default:
                break;
        }
    }
}

~~~
主函数

~~~
package com.icss.test.homework3_change;

import java.util.Scanner;

/**
 * Created by 29185 on 2017/5/25.
 */
public class OneTestto {
    public static void main(String [] args){
        int length = 4;
        System.out.println("选举开始！节目代号及类型名称如下：");
        String [] names = {"小品","独唱","舞蹈","杂技"};
        String [] ids = {"x","d","w","z"};
        JIeMu [] jIeMus = new JIeMu[length];
        for (int i=0;i<jIeMus.length;i++){
            //通过构造函数为数组传递数值
            jIeMus[i] = new JIeMu(names[i],ids[i]);
        }
        //对传递到对象数组的值尽享遍历并输出
        for (JIeMu a:jIeMus) {
            a.showMsg(1);
        }
        Scanner sn = new Scanner(System.in);
        while (true){
            System.out.println("请输入您喜欢的节目代号（输入e结束）：");
            String n = sn.next();
            //下面没想出
            if("e".equalsIgnoreCase(n)){
                System.out.println("选票结束！");
                break;
            }
            // 用else有缺陷，会在不是本次数组中匹配的字母也退出
            int flag = 0;
            for (JIeMu a:jIeMus) {
                if(a.isSameCode(n)){
                    a.addTicket();
                    flag = 1;
                    break;
                }
            }
            if (flag==0){
                System.out.println("选票无效请重新输入！");
            }
        }
        //排序
        for (int i = 0;i<length-1;i++){
            for(int j = 0;j<length-i-1;j++){
                if(jIeMus[j].getTicket()<jIeMus[j+1].getTicket()){
                    JIeMu temp = jIeMus[j];
                    jIeMus[j]  = jIeMus[j+1];
                    jIeMus[i] = temp;
                }
            }
        }
        //进行数组的输出（由大到小）
        for (JIeMu a:jIeMus) {
           a.showMsg(2);
        }
        jIeMus[0].showMsg(3);
    }
}

~~~

##此题重要的编程思想
 
- 每一个类都能创建一个对象数组，那么这个对象数组只能用于装这个类型的对象。但是我们知道，**每个类的属性都是基本类型**而基本类型可以创建自己的类型数组。**所以我们就可以通过for循环来为对象数组赋值每个对象--对象也用数组来赋值**

```
 String [] names = {"小品","独唱","舞蹈","杂技"};
        String [] ids = {"x","d","w","z"};
        JIeMu [] jIeMus = new JIeMu[length];
        for (int i=0;i<jIeMus.length;i++){
            //通过构造函数为数组传递数值
            jIeMus[i] = new JIeMu(names[i],ids[i]);
        }
```
-  for循环的缺陷

```
int flag = 0;
for (JIeMu a:jIeMus) {
    if(a.isSameCode(n)){
        a.addTicket();
        flag = 1;
        break;
    }
}
if (flag==0){
    System.out.println("选票无效请重新输入！");
}

/判断输入内容是否在我们对象中（在这里是对象数组）（是否合法）
/* public boolean isSameCode(String code){
        return this.id.equalsIgnoreCase(code);
    }*/
```

- `boolean isSameCode`思想
当我们唱票的时候，遍历我们定义的数组（里面包含了所有类型）因为数组是每个类型的票都有定义，所以当输入条件又符合的时候就直接跳出循环（接着向下循环没有意义）**在这里如果用if else判断是否合法，那么只要输入的不是该次循环该数组中的存储内容，他就会执行else（肯定会执行3此else）和我们要求不符合，所以这里添加了一个flag用于跳出循环**

### 泛型的一个利用方法
在泛型形参中添加类型约束 如： `ArrayList<Student> arrayList = new ArrayList();`
可以利用foreach间接的将ArrayList转换类型,利用该类型的方法:
`for(Student st : arrayList){ System.out.println(st.getName());}`

#线程编程之生产者消费者

经验总结：
自己的代码：
-------------------------
Customer 消费者
```
package OnClass.Thread.ProAndCus;

/**
 * Created by 29185 on 2017/6/8.
 */
public class Customer extends Thread{
    int num;
    @Override
    public void run() {
        get(num);
    }
    public void get(int num) {
        synchronized (Customer.class){
        //仓库没有空间，可以取东西
        if (num <= Store.getNum() && Store.getNum() >= 0) {
            Store.deleteStroe("something");
            Store.deleteNum(num);
            this.notifyAll();
            System.out.println("仓库别去走了东西,现在有" + Store.getNum() + "产品");

        } else {
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    }
}

```
生产者
```
package OnClass.Thread.ProAndCus;

/**
 * Created by 29185 on 2017/6/8.
 */
public class Producter extends Thread{
    int num;
    @Override
    public void run() {
        set(num);
    }
    public   void set(int num) {
        synchronized (Producter.class){
        //仓库还有空间可以添加
        if (Store.getNum() + num <= Store.getSize()) {
            Store.setStore("somthing");
            Store.addNum(num);
            this.notifyAll();
            System.out.println("进行了生产，一共有" + Store.getNum() + "还可以添加" + (Store.getSize() - Store.getNum()));
        } else {
            //仓库没有空间了
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    }
}

```
仓库
```
package OnClass.Thread.ProAndCus;

import java.util.ArrayList;

/**
 * Created by 29185 on 2017/6/8.
 */
public class Store {
    public static int num = 0;
    public static final int size = 100;
    public static ArrayList<String> store = new ArrayList<>();

    public static int getNum() {
        return num;
    }
    public ArrayList<String> getStore() {
        return store;
    }

    public static int getSize() {
        return size;
    }

    public static void addNum(int num) {
        Store.num += num;
    }
    public static void deleteNum(int num){
        Store.num -= num;
    }

    public static void setStore(String store) {
        Store.store.add(store);
    }
    public static void deleteStroe(String store){
        Store.store.remove(store);
    }
}

```
执行：
```
package OnClass.Thread.ProAndCus;

/**
 * Created by 29185 on 2017/6/8.
 *
 * 为什么会有问题：
 * 1.线程只能自己等，不能让别人等，等完以后才能去执行，执行完唤醒
 * 2.
 *
 */
public class Test {
    public static void main(String[] args) {
        Store store = new Store();
        Producter p1 = new Producter();
        Producter p2 = new Producter();
        Producter p3 = new Producter();
        Producter p4 = new Producter();
        Customer c1 = new Customer();
        Customer c2 = new Customer();
        Customer c3 = new Customer();
        p1.set(20);
        p2.set(10);
        p3.set(30);
        p4.set(20);
        c1.get(10);
        c2.get(20);
        c3.get(30);

        p1.start();
        p2.start();
        p3.start();
        p4.start();
        c1.start();
        c2.start();
        c3.start();



    }
}

```
**总结：
 1.线程只能自己等，不能让别人等，等完以后才能去执行，执行完唤醒（注意if条件）
 2.wait()后他会卡在那里，只有不卡了（不满足条件，内存释放后）他就会接着语句向下执行
 3.线程同步：synchronized 修饰的是那些同一类型的不同对象，以此来解决他们之间的冲突**

--------------------------
老师给的答案：
仓库类
```
package com.lzc.xxoo;

import java.util.ArrayList;
import java.util.List;

public class Ck {
	//用来保存商品
	private List list=new ArrayList();
	//设定库存数量
	private final int size=100;
	
	//同步 避免其他方法 同时调用
	public synchronized void add(int num){
		//如果发现 库存够了
		if(list.size()+num>size){
			System.out.println("仓库够了");
			
			try {
				//当前线程等待
				this.wait();
				
			} catch (InterruptedException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		}
		//
		for(int i=0;i<num;i++){
			list.add("东西");		
		}
		//唤醒其他线程
		this.notifyAll();
		
		System.out.println("添加之后的库存="+list.size());
			
	}
	
	public synchronized void qu(int num){
		
		//如果发现 商品不足
		if(num>list.size()){
				try {
					//当前等待
					this.wait();
				} catch (InterruptedException e) {

					e.printStackTrace();
				}

		}
		
		for(int i=0;i<num;i++){
			list.remove("东西");
		}
		//唤醒其他线程
		this.notifyAll();
		
		System.out.println("取完之后的库存="+list.size());
	}
	
	

}

```
消费者

```
package com.lzc.xxoo;
//消费者
public class Customer extends Thread{
	private int num;
	private Ck ck;
	
	public Ck getCk() {
		return ck;
	}

	public void setCk(Ck ck) {
		this.ck = ck;
	}

	public int getNum() {
		return num;
	}

	public void setNum(int num) {
		this.num = num;
	}

	@Override
	public void run() {
		
		ck.qu(num);
		
	}
	
	

}

```
生产者
```
package com.lzc.xxoo;
//生产者
public class Producter extends Thread{
	
	private int num;
	private Ck ck;
	
	@Override
	public void run() {
		ck.add(num);
	}

	public int getNum() {
		return num;
	}

	public void setNum(int num) {
		this.num = num;
	}

	public Ck getCk() {
		return ck;
	}

	public void setCk(Ck ck) {
		this.ck = ck;
	}

}

```
测试
```
package com.lzc.xxoo;

public class Test {
	
	public static void main(String[] args) {
		Ck ck=new Ck();
		
		Producter p1=new Producter();
		
		Producter p2=new Producter();
		Producter p3=new Producter();
		Producter p4=new Producter();
		Producter p5=new Producter();
		
		p1.setCk(ck);
		p1.setNum(10);
		
		p2.setCk(ck);
		p2.setNum(50);
		
		p3.setCk(ck);
		p3.setNum(20);
		
		
		p4.setCk(ck);		
		p4.setNum(30);
		
		p5.setCk(ck);		
		p5.setNum(45);
		
		
		Customer c1=new Customer();
		Customer c2=new Customer();
		Customer c3=new Customer();
		
		c1.setCk(ck);
		c1.setNum(40);
		
		c2.setCk(ck);
		c2.setNum(10);
		
		c3.setCk(ck);
		c3.setNum(80);
		
		
		p1.start();
		p2.start();
		p3.start();
		p4.start();
		p5.start();
		
		
		c1.start();
		c2.start();
		c3.start();
		
	}

}

```


#网络编程（难点） -----------   图书管理
```
简述一下思想：
1.s.accept();是服务器用来监听访问的，只要有访问就往下执行了，如果没有循环，下面的语句只能执行一次
2.最外层要有一个一直监听传来的FlagAndData 类，循环实现！
3.传递都用的是FlagAndData 类，因为他包含一个flag，用于服务端识别访问的方法；另一个list可以往里面存放任何类型数据。
4.可以在方法中，传出数据后就直接获取数据
5.每一个不同实现都是一个方法


冷浩然：方法参数可以传Socket类型，方便！
```

实体类

```
//图书 -- 真正交互类
public class Book implements Serializable{
    private String name;
    private int id;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return name + id;
    }
}

//用户 -- 真正交互类
public class User implements Serializable{
    private String name;
    private String pwd;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPwd() {
        return pwd;
    }

    public void setPwd(String pwd) {
        this.pwd = pwd;
    }
}
//自定义类---这个类是充当桥梁的交互类
（用于装flag--用于服务器鉴别操作,一个数组--传递Object“也就是任何东西哦，最好还是数组列表”）



public class FlagAndData implements Serializable{
    private int flag;
    //这个要写成Object类型，因为传递的数据不只一个类型
    private List<Object> ArrayList = new ArrayList();

    public int getFlag() {
        return flag;
    }

    public void setFlag(int flag) {
        this.flag = flag;
    }

    public List<Object> getArrayList() {
        return ArrayList;
    }

    public void setArrayList(List<Object> arrayList) {
        ArrayList = arrayList;
    }
}
```
客户端
```
public class BookClient {
    public static BookClient bookClient = new BookClient();
    FlagAndData flagAndData = new FlagAndData();
    public static void main(String[] args) {

            try {
                //建立一个套接字
                Socket socket = new Socket("127.0.0.1",9999);
                while (true){
                        //准备写出数据，传到服务器
                    ObjectOutputStream oos = new ObjectOutputStream(socket.getOutputStream());
                    //接受flag数据，做出相应的操作

                    //正式登录
                    FlagAndData userPass = bookClient.login();
                    oos.writeObject(userPass);
                    System.out.println("客户端传出成功！");
                    /**
                     * 需要注意的是下面的接受数据只要写在前面客户端就会一直等待
                     */
                    InputStream is = socket.getInputStream();
                    int flag =0;
                    flag = is.read();
                    if(flag==0) {
                        System.out.println("登录成功！");
                        show();
                        break;
                    }else {
                        continue;
                    }
                }
            } catch (IOException e) {
                e.printStackTrace();
            }

    }
    //选项显示
    public static void show() {
        Scanner scanner = new Scanner(System.in);
        while (true){
            System.out.println("请输入想执行的操作\n1.录入图书信息\n2.查看图书信息\n3.删除图书信息\t4.更改图书信息");
            int num = scanner.nextInt();
            switch (num) {
                case 1:
                    Socket socket = null;
                    try {
                        socket = new Socket("127.0.0.1", 9999);
                        //准备写出数据，传到服务器
                        ObjectOutputStream oos = new ObjectOutputStream(socket.getOutputStream());
                        FlagAndData flagAndData = addBook();
                        oos.writeObject(flagAndData);
                        oos.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                    break;
                case 2:
                    checkBook();
                    break;
                case 3:
                    deleteBook();
                    break;
                case 4:
                    changeBook();
                    break;
            }
        }
    }
    public FlagAndData login(){
        FlagAndData flagAndData = new FlagAndData();
        Scanner input = new Scanner(System.in);
        //注册功能，建立用户实体
        User user = new User();
        System.out.println("欢迎来到登录界面！");
        System.out.println("请输入用户名：");
        user.setName(input.next());
        System.out.println("请输入密码：");
        user.setPwd(input.next());
        List userList = new ArrayList();
        userList.add(user);
        flagAndData.setFlag(0);
        flagAndData.setArrayList(userList);
        return flagAndData;
    }
    public static FlagAndData addBook(){
        FlagAndData flagAndData = new FlagAndData();
        List bookList = new ArrayList();
        while (true) {

            Scanner input = new Scanner(System.in);
            //注册功能，建立用户实体
            Book book = new Book();
            System.out.println("录入图书：");
            System.out.println("请输入图书名：");
            book.setName(input.next());
            System.out.println("请输入图书编号：");
            book.setId(input.nextInt());
            bookList.add(book);
            flagAndData.setFlag(1);
            flagAndData.setArrayList(bookList);
            System.out.println("是否继续输入  Y/N");
            if(input.next().equalsIgnoreCase("n")){
                break;
            }else {
                continue;
            }
        }
        return flagAndData;
    }
    public static void checkBook(){
        FlagAndData flagAndData = new FlagAndData();
        flagAndData.setFlag(2);

        try {
            Socket socket = new Socket("127.0.0.1",9999);
            ObjectOutputStream oos = new ObjectOutputStream(socket.getOutputStream());
            oos.writeObject(flagAndData);

            ObjectInputStream ois = new ObjectInputStream(socket.getInputStream());
            List list = (List) ois.readObject();
            for(Object o:list){
                System.out.println("图书编号："+((Book)o).getId()+"-----------图书名："+((Book)o).getName());
            }
            ois.close();
            oos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
    }

    public static void changeBook(){
        FlagAndData flagAndData = new FlagAndData();
        List bookList = new ArrayList();
        Book book = new Book();
        Scanner input = new Scanner(System.in);
        System.out.println("请输入要修改的图书编号：");
        book.setId(input.nextInt());
        System.out.println("请输入修改后的图书名：");
        book.setName(input.next());

        flagAndData.setFlag(4);
        bookList.add(book);
        flagAndData.setArrayList(bookList);

        try {
            Socket socket = new Socket("127.0.0.1",9999);
            ObjectOutputStream oos = new ObjectOutputStream(socket.getOutputStream());
            oos.writeObject(flagAndData);

            ObjectInputStream ois = new ObjectInputStream(socket.getInputStream());
            List list = (List) ois.readObject();
            for(int i = 0 ; i<list.size();i++){
                Book book1 = (Book) list.get(i);
                System.out.println("图书编号："+book1.getId()+"-----------图书名："+book1.getName());
            }
           /* for(Object o:list){
                System.out.println(((Book)o).getId()+"-----------"+((Book)o).getName());
            }*/
            ois.close();
            oos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
    }

    public static void deleteBook(){
        FlagAndData flagAndData = new FlagAndData();
        List bookList = new ArrayList();
        Book book = new Book();
        Scanner input = new Scanner(System.in);
        System.out.println("请输入图书编号：");
        book.setId(input.nextInt());
        flagAndData.setFlag(3);
        bookList.add(book);
        flagAndData.setArrayList(bookList);

        try {
            Socket socket = new Socket("127.0.0.1",9999);
            ObjectOutputStream oos = new ObjectOutputStream(socket.getOutputStream());
            oos.writeObject(flagAndData);

            ObjectInputStream ois = new ObjectInputStream(socket.getInputStream());
            List list = (List) ois.readObject();
            for(Object o:list){
                System.out.println("图书编号："+((Book)o).getId()+"-----------图书名："+((Book)o).getName());
            }
            ois.close();
            oos.close();
        } catch (IOException e) {
            e.printStackTrace();
        }catch (ClassNotFoundException e){
            e.printStackTrace();
        }
    }

}

```
服务端
```

public class BookServer {
    private static List list;
    private static List listDelete;
    private static List listChange;
    public static void main(String[] args) {

        try {
            //创建接受套接字
            ServerSocket ss = new ServerSocket(9999);
            while (true) { //while需要写在Socket后面
                //启动
                Socket s = ss.accept();
                //接受对象数据 ois
                ObjectInputStream ois = new ObjectInputStream(s.getInputStream());
                //从客户端读入数据 FlagAndData 类型
                //这个数据一直在和服务器交互，所以不要在外面强制转换，通过flag判断操作，再进行转换
                FlagAndData flagAndData = (FlagAndData) ois.readObject();//问：在下面另起一行直接写ois去作为数据行不行
//-------------------------------------------------------------------------------------------------------------------------------
                //发送对象数据 oos
               // ObjectOutputStream oos = new ObjectOutputStream(s.getOutputStream());在这里写有错，哪用在哪写；
                //flag
                int flag = flagAndData.getFlag();

                if (flag == 0) {
                    //这里要一步一步的去转化，因为得到的是一个List数组里表
                    List list = flagAndData.getArrayList();
                    /**
                     * ------------------这里要写get()才能类型转换
                     */
                    User user = (User) list.get(0);
                    if (user.getName().equals("zzx") && user.getPwd().equals("123")) {
                        System.out.println("登录成功！");
                        flag = 0;
                    } else {
                        System.out.println("登录失败！");
                    }
                }
                //添加
                if(flag==1){
                    list = flagAndData.getArrayList();
                    for(Object v:list){
                        System.out.println(((Book)v).getName());
                    }
                    //问：如何多次存储，读取都不会有冲突？
                }
                //查看
                if(flag==2){
                    ObjectOutputStream oos = new ObjectOutputStream(s.getOutputStream());
                    oos.writeObject(list);
                }
                //删除
                if(flag==3){
                    listDelete = flagAndData.getArrayList();
                    Book book = (Book) listDelete.get(0);
                    for(Object v:list){
                        if(((Book)v).getId()==(book.getId())){
                            list.remove(v);
                            break;
                        }
                    }
                    ObjectOutputStream oos = new ObjectOutputStream(s.getOutputStream());
                    oos.writeObject(list);
                }
                //更改
                if (flag==4){
                    listChange = flagAndData.getArrayList();
                    Book book = (Book) listChange.get(0);
                    for(Object v:list){
                        if(((Book)v).getId()==(book.getId())){
                            int num = list.indexOf(v);
                            list.set(num,book);
                            break;
                        }
                    }
                    ObjectOutputStream oos = new ObjectOutputStream(s.getOutputStream());
                    oos.writeObject(list);
                }
                OutputStream os = s.getOutputStream();
                //最后把flag数据返回作为，客户端显示的依据
                os.write(flag);
                System.out.println("以输出");
            }
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

```