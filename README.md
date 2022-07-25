# SM3
Project: do your best to optimize SM3 implementation

【代码说明】

SM3消息分组长度512位，对于输入的消息，首先进行消息填充，首先把数据填充至512位的倍数.

填充代码：
![image](https://user-images.githubusercontent.com/105579212/180774242-89fa11d6-442f-4c6a-89f2-f945c3285d47.png)
数据填充规则：先填充一个“1”，后面加上k个“0”。其中k是满足(n+1+k) mod 512 = 448的最小正整数，然后再追加64位的数据长度。得到的一个512位数据分组，将其划分为16个消息字，并且作为生成的132个消息字的前十六个，再用这十六个消息字递推生成剩余的116个消息字。

消息扩展：
![Screenshot_20220725_195130_net csdn csdnplus](https://user-images.githubusercontent.com/105579212/180771633-c0769ace-990c-4599-989e-0b61c1243081.png)
然后使用消息扩展得到的消息字进行运算，初值IV被放在A、B、C、D、E、F、G、H八个32位变量中，压缩函数将这八个变量进行六十四轮相同的计算：
![Screenshot_20220725_195354_net csdn csdnplus](https://user-images.githubusercontent.com/105579212/180772383-5b573673-5726-4d6b-8802-1c4d7a7227a3.png)
迭代压缩：
![image](https://user-images.githubusercontent.com/105579212/180774869-5179fbde-f117-46dc-a5b6-259f36092f6d.png)
最后，再将计算完成的A、B、C、D、E、F、G、H和原来的A、B、C、D、E、F、G、H分别进行异或，就是压缩函数的输出。这个输出再作为下一次调用压缩函数时的初值。依次类推，直到用完最后一组132个消息字为止。

将得到的A、B、C、D、E、F、G、H八个变量拼接输出，就是SM3算法的输出。

【运行截图】
![image](https://user-images.githubusercontent.com/105579212/180767391-49797233-701e-4310-b31e-fb1505ab24cd.png)
