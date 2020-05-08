# 虎符

## chall

> https://bbs.pediy.com/thread-248495.htm

~~~
[*] '/home/root0/pratice/2020hf/chall'
    Arch:     amd64-64-little
    RELRO:    Full RELRO
    Stack:    Canary found
    NX:       NX enabled
    PIE:      PIE enabled
~~~

![image-20200420212142876](F:\CTF\2020虎符\wp.assets\image-20200420212142876.png)

任意地址写3字节,其中常用gadget都被禁用了

> one_gadget file --level 1

上述命令可以找到其他可以用的one_gadget，

要点:**_rtld_global._dl_rtld_lock_recursive 为 onegadget**但是找到的one_gadget还是需要偏移少许的，只要它前面的汇编操作不影响它的函数执行，有少许偏移还是可以Getshell的。

## SecureBox

~~~
[*] '/home/root0/pratice/2020hf/Untitled Folder/chall'
    Arch:     amd64-64-little
    RELRO:    Full RELRO
    Stack:    Canary found
    NX:       NX enabled
    PIE:      PIE enabled
~~~

这个题总的就是惩罚那些总是f5的，hh

![image-20200421121535529](F:\CTF\2020虎符\wp.assets\image-20200421121535529.png)

我们传入的size的低四位进行了比较，但是存入的时候确实整个全部存入进去的

![image-20200421121748586](F:\CTF\2020虎符\wp.assets\image-20200421121748586.png)

同时我们可以看到在，enc的输入过程中用的是size 和 offset 的和进行输入，那么我么就可以构造一个合适的大size实现任意写，这就很简单了。。。

