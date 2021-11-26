---
title: 二维码怎么生成
date: 2021-8-26 17:23:00
categories: 
- 计算机
tags:
---
QR code，Quick Response，一种矩阵条形码，二维条形码，在1994年由供职于日本电装公司Denso Wave(丰田子公司)一名职员腾弘原（Masahiro Hara）发明，灵感来源于围棋，用于追踪流水线上的汽车，二维码之所以能快速在汽车制造领域外流行是因为自身的快速读取性，高存储性，更低的容错率，不需要特殊的设备读取。

![image](https://5b0988e595225.cdn.sohucs.com/images/20180202/5388bfb902134e5d9fca2dbf2ea739dc.jpeg)

![image](https://i.guim.co.uk/img/media/69452cfee35f2027d9b375e79cea482f59b540d5/0_376_2667_3333/master/2667.jpg?width=445&quality=45&auto=format&fit=max&dpr=2&s=e4076f0ee84d4bf1231d97d027ebcb81)

![image](https://qvc.scene7.com/is/image/QVC/t/14/t135114.001?$aempdlarge$)



二维码里可包含地理信息，身份标识，网页地址，是对这些信息进行了编码

可编码的原始信息可分为四种：

| 编码模式     | 内容                                                         |
| ------------ | ------------------------------------------------------------ |
| Numeric      | 1234567890                                                   |
| Alphanumeric | ABCDE.....Z   1234567890                                     |
| Byte         | 0000111100001111                                             |
| Kanji        | 漢字の部首・画数・読み方・筆順・意味などを調べることができる漢字辞典サイトで |



每一种模式使用不同的方法把text转换为比特，尽可能使用效率高的方法，编码后的结果是一串比特，8bit为一个单位，称为data codeword。



### 二维码拆分

![image](https://cdn4.explainthatstuff.com/qr-code-barcode-features.png)

![image](https://www.thonky.com/qr-code-tutorial/function-patterns2.png)





1 .**Quiet zone**: 二维码存放的区域，白色底板，用来和其他的图案隔离开来，比如被玷污的信封上，报纸上或者有过摩擦的纸箱表面

2.**Finder patterns**：左上，右上，左下的三个黑白正方形，用来确认是否为二维码，以及二维码的旋转方向

3.**Alignment pattern**: 在非正常情况下用来确保可以正常解码，比如印在凸面上，扫描角度不正等

4.**Timing pattern**:紫色连线部分，小黑白方块组成，用来辅助确认二维码里具体的信息（data cell），尤其是二维码污损的情况下

5.**Version infomation**:绿色部分，用来确认版本信息

6.**Data Cells**:剩余的黑白点部分，全为具体数据



### 容错率

| Error Correction Level | Error Correction Capability |
| :--------------------: | --------------------------- |
|        L  (low)        | Recovers 7% of data         |
|       M (medium)       | Recovers 15% of data        |
|      Q (quarter)       | Recovers 25% of data        |
|        H (high)        | Recovers 30% of data        |

容错率的特点是在原始数据后面加上Reed-Solomon Code。打个比方，一段原始数据里包括100个codeword，需要修复50个，那么需要在数据尾部挂上100个Reed-Solomon code（两倍），这样下来总数为200codeword，容错率为25%，容错等级为Q。也可以认为刚才的例子容错率为50%，鉴于在通常情况下数据部分会污损，所以还是按25%来。容错率越高，数据越大

PS：[Reed-Solomon Code](https://www.qrcode.com/en/about/error_correction.html/) 是一种在制作音乐CD领域较为常用的数学方法，一开始发明用来卫星或者星际通讯降噪，可以在比特级纠错

## 确定数据使用的最小版本

最小的二维码为21 * 21像素，最大是177 * 177像素，不同的尺寸代表不同版本，21 * 21为version 1，25 * 25为version 2，4个像素为一个步进，以此类推，177 * 177为version 40。

每一个版本都有数据容量上限，数据容量取决于编码的信息长度和纠错级别，[字符容量表](https://www.thonky.com/qr-code-tutorial/character-capacities)展示了每个版本不同纠错级别的容量

打个比方，**HELLO WORLD**包含11个字符，使用Q级别纠错，版本1 **Alphanumeric**最大容量是16字符，那么版本一就是**HELLO WORLD**最低版本，依次类推

下表是二维码数据容量的上限

| Encoding Mode | Maximum number of characters a 40-L code can contain in that mode |
| :------------ | :----------------------------------------------------------- |
| Numeric       | 7089 characters                                              |
| Alphanumeric  | 4296 characters                                              |
| Byte          | 2953 characters                                              |
| Kanji         | 1817 characters                                              |

### 添加模式标识

每一种编码模式机器需要通过在数据前添加标识来确定，**HELLO WORLD**的编码代码为表格第二行，0010

| Mode Name         | Mode Indicator |
| :---------------- | :------------- |
| Numeric Mode      | 0001           |
| Alphanumeric Mode | 0010           |
| Byte Mode         | 0100           |
| Kanji Mode        | 1000           |
| ECI Mode          | 0111           |

### 添加个数标识

个数标识表示字符串长度，**HELLO WORLD**长度为11，二进制1011，版本1的比特位长度为9，在左边补齐0，结果为 00000 1011，添加在模式标识后为 0010，00000 1011

下面是各版本规定的比特位长度

#### Versions 1 - 9

| Mode         | Bits |
| ------------ | ---- |
| Numeric      | 10   |
| Alphanumeric | 9    |
| Byte         | 8    |
| Japanese     | 8    |

#### Versions 10 - 26

| Mode         | Bits |
| ------------ | ---- |
| Numeric      | 12   |
| Alphanumeric | 11   |
| Byte         | 16   |
| Japanese     | 10   |

#### Versions 27 - 40

| Mode         | Bits |
| ------------ | ---- |
| Numeric      | 14   |
| Alphanumeric | 13   |
| Byte         | 16   |
| Japanese     | 12   |

### 真实数据编码

以**HELLO WORLD** Alphanumeric模式为例，参考编码表为

```
0 0
1 1
2 2
3 3
4 4
5 5
6 6
7 7
8 8
9 9
A 10
B 11
C 12
D 13
E 14
F 15
G 16
H 17
I 18
J 19
K 20
L 21
M 22
N 23
O 24
P 25
Q 26
R 27
S 28
T 29
U 30
V 31
W 32
X 33
Y 34
Z 35
  36 (space)
$ 37
% 38
* 39
+ 40
- 41
. 42
/ 43
: 44
```

把字符串拆分为如下形式,O和空格在一起

```
HE,LL,O ,WO,RL,D
```

找到对应的数字

H → 17
E → 14

第一个乘以45，加第二个

(45 * 17) + 14 = 779

转换为11bit长的字符串，左边补0

779 → 01100001011

以此类推得到所有的数据，最后一位D -> 13 转换长度为6比特 001101

| Mode Indicator | Character Count Indicator | Encoded Data                                                 |
| :------------- | :------------------------ | :----------------------------------------------------------- |
| 0010           | 000001011                 | 01100001011 01111000110 10001011100 10110111000 10011010100 001101 |

### 转换为8-bit CodeWord

二维码要求数据必须填满，参考[纠错表](https://www.thonky.com/qr-code-tutorial/error-correction-table)，此处，我们采用的是版本一，Q级别，可以有13个CW，每个CW为8-bit，总容量为13*8=104bit，到了这一步，我们的数据总长度为74，离满格还差34，需要在尾部添加四个0，最多四个，如果数据长度为102，则补齐两个0，以此类推，到现在我们的数据为

| Mode Indicator | Character Count Indicator | Encoded Data                                                 | Terminator |
| :------------- | :------------------------ | :----------------------------------------------------------- | :--------- |
| 0010           | 000001011                 | 01100001011 01111000110 10001011100 10110111000 10011010100 001101 | 0000       |

### 拆分补齐数据，使之长度为8的倍数

74 + 4 = 78bit，在末尾添加00成为80bit

前：

00100000 01011011 00001011 01111000 11010001 01110010 11011100 01001101 01000011 010000

后：

00100000 01011011 00001011 01111000 11010001 01110010 11011100 01001101 01000011 010000**00**

距离104还差24bit，使用Pad bytes继续填充

| 236      | 17       |
| -------- | -------- |
| 11101100 | 00010001 |

00100000 01011011 00001011 01111000 11010001 01110010 11011100 01001101 01000011 01000000 **11101100 00010001 11101100**

236 - 17 - 236 - 17 如此循环下去，直到填满为止，对应的十进制为

32,91,11,120,209,114,220,77,67,64,236,17,236



### 数据纠错编码

- 数据分组

- [Reed-Solomon算法](https://www.thonky.com/qr-code-tutorial/error-correction-coding)，包含多项式、伽罗瓦群论、对数、XOR计算等组合方法生成

  ![image](https://s3-us-west-2.amazonaws.com/courses-images-archive-read-only/wp-content/uploads/sites/924/2015/11/25201522/CNX_Precalc_revised_eq_12.png)

  ![image](https://slideplayer.com/slide/9698581/31/images/12/Galois+Field+Example+Example%3A+Multiplying+110+and+101.jpg)



![image](https://i.pcmag.com/imagery/encyclopedia-terms/xor-xor.fit_lim.size_1050x.gif)

根据[算法](https://www.thonky.com/qr-code-tutorial/show-division-steps?msg_coeff=32%2C91%2C11%2C120%2C209%2C114%2C220%2C77%2C67%2C64%2C236%2C17%2C236&num_ecc_blocks=13)产生的纠错码为

168 72 22 82 217 54 156 0 46 15 180 122 16

合起来为

|         | Col 1 | Col 2 | Col 3 | Col 4 | Col 5 | Col 6 | Col 7 | Col 8 | Col 9 | Col 10 | Col 11 | Col 12 | Col 13 |
| :------ | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :---- | :----- | :----- | :----- | ------ |
| Block 1 | 32    | 91    | 11    | 120   | 209   | 114   | 220   | 77    | 67    | 64     | 236    | 17     | 236    |
| Block 2 |       |       |       |       |       |       |       |       |       |        |        |        |        |
| ECC1    | 168   | 72    | 22    | 82    | 217   | 54    | 156   | 0     | 46    | 15     | 180    | 122    | 16     |
| ECC2    |       |       |       |       |       |       |       |       |       |        |        |        |        |

内容连起来，转换为二进制，类似于

```
01000011111101101011011001000110
```

### 尾部添加0

不同的版本在末尾添加0补全

| QR Version | Required Remainder Bits |
| :--------- | :---------------------- |
| 1          | 0                       |
| 2          | 7                       |
| 3          | 7                       |
| 4          | 7                       |
| 5          | 7                       |
| 6          | 7                       |
| 7          | 0                       |
| 8          | 0                       |
| 9          | 0                       |
| 10         | 0                       |
| 11         | 0                       |
| 12         | 0                       |
| 13         | 0                       |
| 14         | 3                       |
| 15         | 3                       |
| 16         | 3                       |
| 17         | 3                       |
| 18         | 3                       |
| 19         | 3                       |
| 20         | 3                       |
| 21         | 4                       |
| 22         | 4                       |
| 23         | 4                       |
| 24         | 4                       |
| 25         | 4                       |
| 26         | 4                       |
| 27         | 4                       |
| 28         | 3                       |
| 29         | 3                       |
| 30         | 3                       |
| 31         | 3                       |
| 32         | 3                       |
| 33         | 3                       |
| 34         | 3                       |
| 35         | 0                       |
| 36         | 0                       |
| 37         | 0                       |
| 38         | 0                       |
| 39         | 0                       |
| 40         | 0                       |

在这里我们用第一版，不加零



### 生成矩阵

![image](https://www.thonky.com/qr-code-tutorial/finder.png)

![image](https://www.thonky.com/qr-code-tutorial/finder_example_1.png)

![image](https://www.thonky.com/qr-code-tutorial/finder_example_18.png)

#### 添加分隔线

![img](https://www.thonky.com/qr-code-tutorial/separators.png)

![img](https://www.thonky.com/qr-code-tutorial/separators2.png)

#### 添加对齐图案

![img](https://www.thonky.com/qr-code-tutorial/alignment-pattern.png)

version 2及其以上需要这个图案，经过查表可以得知，以左上角为原点，可以摆放四个位置，(6, 6), (6, 18), (18, 6) and (18, 18)，不能遮挡，故右下角合格

# INCORRECT

![img](https://www.thonky.com/qr-code-tutorial/alignment-exclusion.png)

# CORRECT

![img](https://www.thonky.com/qr-code-tutorial/alignment-correct.png)



![img](https://www.thonky.com/qr-code-tutorial/alignment-example.png)

#### 添加Timing Patterns

![img](https://www.thonky.com/qr-code-tutorial/timing-s.png)![img](https://www.thonky.com/qr-code-tutorial/timing-m.png)

![img](https://www.thonky.com/qr-code-tutorial/timing-l.png)

开始和结束均为黑色

#### 黑色模块和数据保留区

![img](https://www.thonky.com/qr-code-tutorial/format-reserved1.png)![img](https://www.thonky.com/qr-code-tutorial/format-reserved2.png)

左下角黑点 Dark Module和蓝色区域部分Reserved Areas

#### 版本数据区域

![img](https://www.thonky.com/qr-code-tutorial/version-area1.png)![img](https://www.thonky.com/qr-code-tutorial/version-area2.png)

version 7及其以上必须包含版本信息，两个蓝色区域

#### 添加文本数据

![img](https://www.thonky.com/qr-code-tutorial/data-bit-progression.png)

![img](https://www.thonky.com/qr-code-tutorial/upward.png)

![img](https://www.thonky.com/qr-code-tutorial/downward.png)



如果遇到了阻挡，绕过去

![img](https://www.thonky.com/qr-code-tutorial/alignment-modules10.png)

如果遇到了垂直的Timing Pattern,跳过去到下一列

![img](https://www.thonky.com/qr-code-tutorial/timing-modules4.png)

### Data Masking

为什么需要masking，因为要减少复杂度，提升机器的识别率

什么是masking

- 黑白切换

Mask方法

- 只mask数据区域

Mask种类

| Mask Number | If the formula below is true for a given row/column coordinate, switch the bit at that coordinate |
| :---------- | :----------------------------------------------------------- |
|             |                                                              |
| 0           | (row + column) mod 2 == 0                                    |
| 1           | (row) mod 2 == 0                                             |
| 2           | (column) mod 3 == 0                                          |
| 3           | (row + column) mod 3 == 0                                    |
| 4           | ( floor(row / 2) + floor(column / 3) ) mod 2 == 0            |
| 5           | ((row * column) mod 2) + ((row * column) mod 3) == 0         |
| 6           | ( ((row * column) mod 2) + ((row * column) mod 3) ) mod 2 == 0 |
| 7           | ( ((row + column) mod 2) + ((row * column) mod 3) ) mod 2 == 0 |

#### 寻找最佳Mask

每一种mask加上去后进行四种惩罚算法验证，得分最低者为最合适的mask

- The first rule gives the QR code a penalty for each group of five or more same-colored modules in a row (or column).
- The second rule gives the QR code a penalty for each 2x2 area of same-colored modules in the matrix.
- The third rule gives the QR code a large penalty if there are patterns that look similar to the finder patterns.
- The fourth rule gives the QR code a penalty if more than half of the modules are dark or light, with a larger penalty for a larger difference.

这里举第一种惩罚算法为例

![img](https://www.thonky.com/qr-code-tutorial/horizontal-total.png)![img](https://www.thonky.com/qr-code-tutorial/vertical-total.png)

![img](https://www.thonky.com/qr-code-tutorial/qr-masks.png)

350得分最低，选择第一种mask

### 添加格式信息

纠错级别有四个 L M Q H，Maks有八种，一共32种组合

格式信息是一个15-bit长的字符串 

前5个bit包含纠错版本（2-bit）和mask版本（3-bit）

| Error Correction Level | Bits | Integer Equivalent |
| :--------------------- | :--- | :----------------- |
| L                      | 01   | 1                  |
| M                      | 00   | 0                  |
| Q                      | 11   | 3                  |
| H                      | 10   | 2                  |



| Mask Number | If the formula below is true for a given row/column coordinate, switch the bit at that coordinate |
| :---------- | :----------------------------------------------------------- |
|             |                                                              |
| 0           | (row + column) mod 2 == 0                                    |
| 1           | (row) mod 2 == 0                                             |
| 2           | (column) mod 3 == 0                                          |
| 3           | (row + column) mod 3 == 0                                    |
| 4           | ( floor(row / 2) + floor(column / 3) ) mod 2 == 0            |
| 5           | ((row * column) mod 2) + ((row * column) mod 3) == 0         |
| 6           | ( ((row * column) mod 2) + ((row * column) mod 3) ) mod 2 == 0 |
| 7           | ( ((row + column) mod 2) + ((row * column) mod 3) ) mod 2 == 0 |

11000,剩下的十位重新使用Reed-Solomon算法生成ECC code，填进去二维码蓝色区域

![The layout of format string bits, where 14 is the most significant bit and 0 is the least significant bit](https://www.thonky.com/qr-code-tutorial/format-layout.png?a=)

无论哪个版本，格式信息总是在红色的区域

![img](https://www.thonky.com/qr-code-tutorial/format-position-1.png)![img](https://www.thonky.com/qr-code-tutorial/format-position-2.png)



#### 生成版本信息

version 7及其以上版本，必须包含18bit长度的版本信息，6-bit表示版本号，12-bit代表纠错码，同样的算法生成

![img](https://www.thonky.com/qr-code-tutorial/version-location-1.png)![img](https://www.thonky.com/qr-code-tutorial/version-location-2.png)

蓝色区域，3*6格子，下图是一个version 7示例

![img](https://www.thonky.com/qr-code-tutorial/version-example.png)

顺序是从右下到左上填充

| 00   | 01   | 02   |
| ---- | ---- | ---- |
| 03   | 04   | 05   |
| 06   | 07   | 08   |
| 09   | 10   | 11   |
| 12   | 13   | 14   |
| 15   | 16   | 17   |

| 17   | 16   | 15   | 14   | 13   | 12   | 11   | 10   | 9    | 8    | 7    | 6    | 5    | 4    | 3    | 2    | 1    | 0    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 0    | 0    | 0    | 1    | 1    | 1    | 1    | 1    | 0    | 0    | 1    | 0    | 0    | 1    | 0    | 1    | 0    | 0    |

### 添加合适mask（上面已经叙述过）

### 添加quiet zone

### 最终生成 HELLO WORLD 二维码，1-Q,Alphanumeric

![img](https://www.thonky.com/qr-code-tutorial/hello-world-final.png)





完。

![image](https://www.pgyer.com/app/qrcode/lMxO)





附录：

条形码：一维码，一种包含物料详情的机读型的光学标签

![image](data:image/png;base64,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)



ASCII Table:

![image](http://wiki.robotz.com/images/3/37/Asciifull.gif)

![image](https://lessonsforenglish.com/wp-content/uploads/2020/05/Common-Number-Prefixes-Greek-Latin-Meaning-and-Examples.png)

在线进制转换网站 https://tool.lu/hexconvert/

参考：https://www.nayuki.io/page/creating-a-qr-code-step-by-step

https://en.wikipedia.org/wiki/QR_code

https://www.explainthatstuff.com/how-data-matrix-codes-work.html

https://www.thonky.com/qr-code-tutorial/introduction

