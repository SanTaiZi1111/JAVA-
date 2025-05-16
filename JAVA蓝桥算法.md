## 数组

### 1.二分查找

左右指针，取中遍历(//通过左闭右开等条件，看left与right相等这个状态在题目区间是否合法)

`int left = 0, right = nums.length - 1;
        while (left <= right) {
            int mid = (right - left) / 2 + left; `

`              if(nums[mid]==target) {
				return mid;
			}else if(nums[mid]>target) {
				right=mid-1;//看开闭边界区间处理mid还是 mid+1
			}else {
				left=mid+1;
			} ` 

 `}    `

### 2.快慢双指针

> 移除元素27：数组固定，删除某元素，该位置空出来了，索引不变

快指针：寻找删后数组中所**需要**的元素

慢指针：删后数组空位下标（删后需要覆盖的位置）

### 3.滑动窗口

> 一层循环 j 指向终止位置（而非起始位置，否则与暴力无区别）

`int i=0;//起始位置    `

`for(int j=0;j<nums.length;j++) {//j为终止位置,注意遍历边界
        	sum+=nums[j];//收集和
        	while(sum>=target) {
        		int subL=j-i+1;//长度
        		result=Math.min(result,subL);
        		sum-=nums[i];//起始位置后移，减去它的值
        		i++;
        	}
        }`

### 4.滑动窗口最大值

每滑动一次就扔掉(pop)前面一个，加入(push)后面一个

第一次push后，当前状态下最大数之前的略小数都可以弹掉。随后加入下一位，再弹出当前最大数之前的略小数。每次都能取到队列开头一个max数。

​    1   3   -1   -3  5  3  2  1

（1  3）弹出1，写3

（3  -1）这里开始压入滑动数组长度，**写3**

（3  -1  -3）**写3**

（3 -1 -3 5），减首个超窗口长度的，弹出之前所有，**写5**

（5  3）**写5**

（5  3  2）**写5**

（5  3  2  1）弹出5，**写3**

**3  3  5  5  5  3**

ArrayDeque

### 5.前缀和：

前缀和是对从开始到当前索引所有元素的总和

`pre[i]=pre[i-1]+a[i]`//每次算进去一个

通过简单减法可以得到所有子数组和：`pre[j] - pre[i]`

#### k倍区间

`//(pre[j]−pre[i−1])mod k=0
//pre[j]mod k=pre[i−1]mod k`

前缀和来帮助快速计算任意子数组的和





### 6.数字与字符间转换（字符用单引号）

​	大小写字母和数字都有属于本身的ASCLL码：字符的ASCLL顺序：'A' (65) < 'B' (66) < ... < 'Z' (90) < 'a' (97) < 'b' (98) < ... < 'z' (122)

> 常用于比较大小写



小写字母ASCLL比大写字母高32

数字的ASCLL：（0）48到（9）57

字符’a‘转为ASCLL值(97)并减去该值变为0：(int)'a'-97=0；

数字0变字符’0‘，无改动，只变换性质：(char)（num+'0'）

字符'0'变为数字0：(int) c -  '0'







**大写**字母变数字：(int)'A'-65；//将A转换成ASCII， 减65，A映射为0

整数 i 转换为**大写**字符：(char) i +65；



 **小写**字母转**索引**0到25， 字符a[i]改为数字索引：mark[a[i]-'a']  

**数字**0到25 换为**字符**'a'到'z'：c=(char)(i+'a');

### 7.内置函数

Integer.valueOf(s[0]);//将s[0]转为整数

Arrays.sort

Arrays.copy//对数组的操作用Arrays



### 8.库

#### 链表支持任意位置插入：

##### (1)链表：

LinkedList<int[]> que = new LinkedList<>(); //链表，元素是int数组

ArrayList<Integer>[] dd=new ArrayList[t+1]; //dd[]数组，元素是ArrayList<Integer>

> 需要初始化：dd[i] = new ArrayList<Integer>();

que.add(p[1],p);//将p插入链表queue 的p[1]位置（尾部插入）

que.addFirst();//头部插入

## 字符串

### 1.双指针

  ` for(int i=0,j=n-1;i<n/2;i++,j--) {
        	char temp=s[i];//i付出去就空了可以安放其他
        	s[i]=s[j];
        	s[j]=temp;
        }`

`while(l<r) {
			char temp=arr[l];
			arr[l]=arr[r];
			arr[r]=temp;
			l++;
			r--;
			}`

> ^=：按位异或
>
> a^=b 或者a=a^b  交换两个变量的值，无需使用临时变量

### 2.滑动数组指针  

`for(int i=0;i<s.length();i+=2*k) {	        //i到i+k反转	           if(i+k<=s.length()) {	        	//尾指针n-1	        	reverse(arr,i,i+k-1);	        	`

`continue;//合格，前k可以反转，不执行下面函数，执行下一轮	        }	       `

` reverse(arr,i,n-1);//不合格，少于k,剩下的全反转	        	}`

### 3.快慢指针

> 反转字符串中的单词151
>
> 快慢指针去掉多余空格，先反转整体字符串，再逐个反转单词。

快指针：获取符合题目要求的字母

慢指针：获取这些字母后在哪里更新

### 4.KMP

前缀：包含首字母，不包含尾字母的所有子串

后缀：只包含尾字母，不包含首字母

最长相等前 后缀：从前数，从后数相等

> aabaaf   0                     **aa**b**aa**  2     
>
> 前缀表：aa**b**aaf  
>
> ​               0101**2**0
>
> 最长相等前后缀为 2，所以下标跳到索引2

i：后缀末尾位置

j：前缀末尾位置/ i 之前包括 i 的子串最长相等前后缀长度

### 5.内部函数

map.getOrDefault(c,0)//若key为c的value为空，就赋为0，不为空就反应value

map.values()//遍历所有的values

map.put(key,value);

**s.substring(i,j)**//截取子串

**String.format("%02d",a);**//函数：格式化二位整数，不足用前导零补充

String s=String.valueOf(n);//数n转字符串

分割字符串:

//字符串s每300个分割一次分为串数组
		for(int i=0;i<300;i++) {
			int start=i*300;//下一组
			int end=Math.min(start+300,s.length());
			s2[i]=s.substring(start, end);//每行
				}

输入：`sc.hasNext()` 是 Java 中 Scanner 类的一个方法，通常用于检查输入流中是否还有下一个输入项。  while(sc.hasNext){ }

## 贪心

### 1.跳跃游戏二

最少跳跃次数：step，每一步尽量往远跳，看最远覆盖距离cover里跳跃最远的

### 2.优先队列

### 3.比较器排序

（1）.字符串长度排序：` public int compare(String s1, String s2) {                  int lenComp = Integer.compare(s1.length(), s2.length());  ` 

 `         if (lenComp != 0) {                   ` 

 `               return lenComp; // 如果长度不同，按照长度排序    }` 

 `           return s1.compareTo(s2); // 如果长度相同，按照字典序排序              }  `

（2）按照对象属性排序

`Arrays.sort(people, (a, b) -> {
    if (a[0] == b[0]) return a[1] - b[1];
    return b[0] - a[0];
});`//按照首个元素从大到小排序，若首个元素相等按照第二个元素从小到大排序

> 从小到大排序是正序，(a,b)->a-b，是可以的，这个代码的意思是返回a减b，通过结果的正负来排序。

> 针对大数溢出问题可以写成：(a,b)->Integer.compare(a[0], b[0])



##  二叉树

### 基础概念：

#### 一、种类：

满二叉树：节点数量 **2的k次幂-1**

完全二叉树：除了底层以外，其他层都是满的，**底层从左到右连续**。

二叉搜索树：**左子树**所有结点都**小于中间**节点，右子树都大于中间结点。

平衡二叉搜索树：左子树和右子树**高度之差**不能大于1

#### 二、存储方式：

链式存储：左右指针指向下一个元素

线式存储：结点i，左孩子索引（2i+1）  右孩子索引（2i+2）

*构造二叉树：（链表，两个指针左右孩子）

#### 三、遍历：

> 深度优先搜索：前中后序遍历，搜到终点往回退
>
> 广度优先搜索：层序遍历

（1）前序遍历：中左右（中的位置就是名字）

（2）中序遍历：左中右

（3）后序遍历：左右中

#### 四、定义方式：

`public class TreeNode {
		      int val;
		      TreeNode left;
		      TreeNode right;
		      TreeNode() {}
		      TreeNode(int val) { this.val = val; }
	 TreeNode(int val, TreeNode left, TreeNode right) {
		          this.val = val;
		          this.left = left;
		          this.right = right;
		      }
      }`

#### 五、图中边|树的节点

`static class Pair{//邻接表表示图的起止点
		int first,second;
		Pair(int first,int second){
			this.first=first;
			this.second=second;
		}
	}`

图中边：`List edges = new ArrayList<>();
 edges.add(new Pair(1, 2)); // 表示一条从节点1到节点2的边
 edges.add(new Pair(2, 3)); // 表示一条从节点2到节点3的边`

树的节点：`List nodesWithDepth = new ArrayList<>();
 nodesWithDepth.add(new Pair(nodeValue, depth));//节点，对应深度`

### 1.递归前序144

> 步骤：确定递归函数的参数返回值；确定终止条件；确定单层递归的逻辑。

` public List<Integer> preorderTraversal(TreeNode root) {
	        List<Integer> res=new ArrayList<>();
	        pre(root,res);
	        return res;
	    }
	 void pre(TreeNode root,List<Integer> res) {
		 if(root==null) {return;}
		 res.add(root.val);//中
		 pre(root.left, res);//左
		 pre(root.right,res);//右
	 }`

### 2.最小生成树

3.路经总和112

## 数学

### 1.矩阵

（1）加法

（2）乘法

### 2.GCD

`public static int gcd(int a,int b) {//最大公约
		return b==0?a:gcd(b,a%b);
	}`

### 3.LCM

`public static int lcm(int a,int b) {//最大公倍数，路经长短
		return a/gcd(a,b)*b;
	}`

### 4.快速幂

`//快速幂函数:a的b次幂取模
	public static long fp(long a,long b,int m) {
		long res=1;
		while(b>0) {
			if((b&1)==1) {//b是奇数
				res=res*a%m;
			}
			a=a*a%m;//平方底数
			b>>=1;//  b/2
		}
		return res;
	}`

`1 << n` 等价于 ：1乘 2的n次幂

`x >> n`  ：  x除以2的n次幂

### 5.组合数学

排列、组合、递推

杨辉三角：c(i,j)    排列组合阶乘公式，C不包括重复选本身

前n个自然数和：res = (n-1)*n/2 % mod;

循环累乘：`for(int i = 3; i <= n; i++){
 res = res * i % mod;
 }`

### 6.异或：

> 因为a^b=x;所以a^x=b

> 左移操作：1<<20   ：就是1乘以2的20次方

### 7.质因子（数论分块）

左端点:L  右端点：n/n/L

### 8.方差

> 可以转换为：S=(每份单独值的平方**总和 **  / 份数) - 平均值的平方

`for(int i=k;i<num;i++) {//滑动窗口
			sum+=b[i]-b[i-k];
			avr=sum/(double)k;
			sumsqrt+=(b[i]*b[i])-(b[i-k]*b[i-k]);
			S=sumsqrt/(double)k-avr*avr;
			if(S<T) return true;
		}`

### 9.完全平方数

不考虑1：`for(Long s=2L;s*s<=n;s++) {//从2开始，1是完全平方根
		while(n%(s*s)==0) n/=(s*s);		}`

### 10.贡献计算

`for(int i=0;i<len;i++) {
			int left=0;
			int right=0;
			char c=arr[i];`

`//从当前位置左侧遍历，直到遇到相同字符或到达开头，left记录未遇到相同字符数量
			for(int j=i-1;j>=0&&arr[j]!=c;j--) {
				left++;
			}`

`//从当前位置向右遍历，直到遇到相同的字符或到达字符串的末尾，right同理
			for(int j=i+1;j<len&&arr[j]!=c;j++) {
				right++;
			}
			count+=(left+1)*(right+1);
		}`

### 11.逆元

加法逆元：*a*+*b*≡0mod*m*

乘法逆元：*a*⋅*b*≡1mod*m*

​	当gcd(a,m)=1时存在逆元b；a的m-2次幂就是a的逆元

### 12日期问题

闰年：是4的倍数，不是100的倍数。   或   是400的倍数

正常2月28    闰年2月29

### 13.等差素数列

素数：只有1和它本身这两个除数

`public static boolean isPrime(int num){
		for(int i=2;i<=Math.sqrt(num);i++) {
			if(num%i==0) 
				return false;
		}
		return true;
	}`

公理：小于等差素数列的长度的素数的乘积就是该等差素数列的公差。

## BigInteger

比int long范围大，都包含

（1）定义：

​	字符串变大整数：`BigInteger num=new BigIntger("15448363583");`

​	字节数组变大整数：`BigInteger(int signum, byte[] magnitude)`

（2）计算：加add、减subtract、乘multiply、除divide、乘方pow、取模mod

（3）比较：compareTo();

（4）位操作：and按位与、or按位或、xor按位异或

（5）使用样例：BigIntegr a=b.add();

int m=b.intValue()//将b转换成int类型

BigInteger.valueOf(20): 这个方法将 20 包装成一个 BigInteger 对象

### Integer：

Integer.MAX很大很大，不仅仅代表十位数，它再跟其他做加减会溢出

Integer.parseInt(String.valueOf(c));//字符**数组**c[ ]转**字符串**再转为**整数**

Integer.bitCount(m);//整数 **`m`** 的二进制表示中 **`1`** 的位数

### Long型声明记得L

## 图论

### 1.连通块：

`if(map[i][j]=='L') {//走到左边房间，i j对应加减分清楚
			dfs(i,j-1);
		}else if(map[i][j]=='R') {
			dfs(i,j+1);
		}else if(map[i][j]=='U') {
			dfs(i-1,j);
		}else if(map[i][j]=='D') {
			dfs(i+1,j);
		}`

### 2.并查集解决连通性问题（七段码）

（1）Union Find(合并查询)树形数据结构：

​	Find确定元素属于哪个子集，可以用来确定两个元素是否属于同一子集

​	Union将两个子集合并成一个集合

（2）常用代码：

初始化：`int fa[MAXN];//源头上司`

`inline void init(int n) {	`

`for(int i=1;i<=n;i++)`

`fa[i]=i;}`

查询：`int find(int x) {
		if(fa[x]==x)
			return x;
		else {
			return find(fa[x]);
		}
	}`

合并：

路径压缩：

（3）解决问题：

图的连通性

集合的个数

集合中元素的个数

## 递归

break：跳出该层循环

continue：执行该层的下一轮循环

return：直接返回结果
