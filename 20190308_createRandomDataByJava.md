### java下生成随机数的方法

##### １．使用Math.random()
- math.random()生成的是[0.0, 1.0)的伪随机数

```
int a[] = new int[10];
for(int i=0;i<a.length;i++ ) {
	a[i] = (int)(10*Math.random());
	System.out.print(a[i]);
}
```


##### ２．random.nextInt(N)
- 每次从0-N随机选取一个数字拼接字符串返回,生成N位随机数

```
Random random = new Random();
String result="";
for (int i=0;i<6;i++)
{
	result+=random.nextInt(10);
}
System.out.println(result);
```


##### ３．random.nextInt(字符串数组)
- 从字符串数组中任意挑一位循环组成随机数

```
String sources = "0123456789abcdefghijklmnopqrstuvwxyz";
Random rd = new Random();
StringBuffer sb = new StringBuffer();
for (int j = 0; j < 10; j++)
{
	sb.append(sources.charAt(rd.nextInt(sources.length())));
}
System.out.println(sb.toString());
```

- 写法不同但要实现的功能一样

```
Random rd = new Random();
String[] radmon = { "0", "1", "2", "3", "4", "5", "6", "7", "8", "9", "a", "b", "c", "e", "f", "g", "h", "i", "j", "k", "l", "m", "n"};
StringBuffer sb = new StringBuffer();

for (int i = 0; i < 10; i++) {
	String s = radmon[rd.nextInt(radmon.length)];
	sb.append(s);
	System.out.println(s);
}
System.out.println(sb);
```
