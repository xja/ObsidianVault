## 抓包
```
sudo wifite --kill --new-hs -mac --no-wps --skip-crack --no-pmkid #--clients-only

sudo airmon-ng stop wlan0mon
sudo airmon-ng stop wlan1mon
sudo systemctl start NetworkManager
```


[hashcat跑包方法 - zhihu.com](https://zhuanlan.zhihu.com/p/682659342)


## 转换
1、如果你抓到的是hccapx格式，先到：[格式转换](https://www.nnnxxx.cn)，使用在线工具把hccapx转为cap。如果本身的包就是cap格式，则这一步可以省略。
2、有了cap文件以后，我们到hashcat的官方，使用在线工具[cap2hcc22000](https://hashcat.net/cap2hashcat/)把cap转为hashcat格式hc22000
3、hcxpcapngtool转换格式
  `hcxpcapngtool -o hs.hc22000 hs.cap`


## 选项
想要用hashcat跑包，你必须告诉hashcat几方面的信息：

1、用什么方式跑。用字典还是掩码，还是字典和掩码的结合。这个是用-a来指定。

2、跑什么类型的密码。是wifi的，还是office的，还是zip的等等。这个是用-m来指定。

3、跑出来的密码保存到哪里。这个是用-o选项来指定。

4、握手文件在哪里，还有要是跑字典的话，字典文件在哪里。这个直接给出路径就行。


### -a
-a选项有下面几个选择：

-a 0 纯字典破解。

-a 1 两个字典组合破解。比如一个字典里是123，另一个字典里是abc，跑的时候会组合成123abc这个密码（笛卡尔积）。

-a 3 纯掩码破解，字典要是太大放不大，可以用掩码

-a 6 字典加掩码组合。也是做笛卡尔积。

-a 7 掩码加字典组合。做笛卡尔积。

-a 9 [wiki / 关联攻击 - hashcat.net](https://hashcat.net/wiki/doku.php?id=association_attack)


## 例子
1、跑8位纯数字wifi密码，用掩码最合适。
```
.\hashcat.exe   -a  3  -m  22000  -o  found.txt    D:\hash\woshoubao.hc22000   ?d?d?d?d?d?d?d?d
```
2、跑手机号，用字典合适。
```
.\hashcat.exe   -a  0  -m  22000  -o  found.txt    D:\hash\woshoubao.hc22000   D:\zidian\jinanshoujihao.txt
```
3、跑9到10位纯数字，用掩码最合适。
```
.\hashcat.exe   -a  3  -m  22000  -o  found.txt  --increment  --increment-min 9   --increment-max  10  D:\hash\woshoubao.hc22000    ?d?d?d?d?d?d?d?d?d?d
```
4、跑前面一个小写字母后面是手机号，比如a15966670284
```
.\hashcat.exe   -a  7  -m  22000  -o  found.txt   D:\hash\woshoubao.hc22000  ?l  D:\zidian\jinanshoujihao.txt
```
5、跑前面一个大写字母或小写字母后面是手机号，比如a15966670284或A15966670284
```
.\hashcat.exe   -a  7  -m  22000  -o  found.txt   --custom-charset1  ?u?l  D:\hash\woshoubao.hc22000  ?1  D:\zidian\jinanshoujihao.txt
```
6、跑前面是手机号后面是一个大写字母或小写字母，比如15966670284a或15966670284A
```
.\hashcat.exe   -a  6  -m  22000  -o  found.txt   --custom-charset1  ?u?l  D:\hash\woshoubao.hc22000
```


## 会话
```
hashcat --session MIFI2080 -a 3 -m 22000 handshake_MIFI2080_00-90-4C-35-0C-A9_2025-08-21T21-04-40.hc22000 8-14--lud--1-4--1-4--7-11.txt
hashcat --session MIFI2080 --restore
```
