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