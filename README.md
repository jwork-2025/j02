# J02

下图(https://raw.githubusercontent.com/jwork-2025/j02/main/example/resources/bubble.jpeg) 中有一些泡泡

![](https://raw.githubusercontent.com/jwork-2025/j02/main/resources/bubble.jpeg)


下图(https://i.postimg.cc/02PpNtdJ/hulu-Bubble-Sorter.png)中也有一些泡泡

![](https://i.postimg.cc/02PpNtdJ/hulu-Bubble-Sorter.png)

这两张图你看得出区别么？你应该是看不出来的。但其实两张图并不一样，后者为一张“隐写术图”（[Steganography](https://zh.wikipedia.org/zh/隐写术))。

我将一个实现冒泡排序的BubbleSorter类的字节码编码进了第一张泡泡图片中，得到了第二张图。

然后`j02`中的`World()`构造函数中的代码即可进行改写：

```java
...
    SteganographyClassLoader loader = new SteganographyClassLoader(
            new URL("https://i.postimg.cc/02PpNtdJ/hulu-Bubble-Sorter.png"));

    Class c = loader.loadClass("hulu.BubbleSorter");

    Sorter sorter = (Sorter) c.newInstance();

    sorter.load(bros);
    sorter.sort();
...
```

请尝试运行代码（注意`lib`目录下存在一个jar文件，需要被包含在工程的classpath中），理解其含义并完成以下任务：

1. 写下对代码工作原理的理解；
2. 将自己在`j01`中实现的Sorter（冒泡排序除外）编码进自选图片得到隐写术图，并用classloader加载Sorter，得到排序结果。
3. 联系另一位同学，尝试加载他的隐写术图，看是否得到正确的排序过程。
4. 请编写README.md，记录实验过程与结果。

**One more thing.** 当前`.github/workflows/j02.yaml`的执行可以通过，但实际上并没有运行成功（虽然你在自己本地可以成功运行示例代码）：

```bash
Run xvfb-run -a java Main &
Exception in thread "main" java.lang.ClassNotFoundException
	at classloader.SteganographyClassLoader.findClass(SteganographyClassLoader.java:37)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:592)
	at java.base/java.lang.ClassLoader.loadClass(ClassLoader.java:525)
	at hulu.World.<init>(World.java:57)
	at WorldScreen.<init>(WorldScreen.java:12)
	at Main.<init>(Main.java:20)
	at Main.main(Main.java:50)
```

请尝试找出原因并解决。