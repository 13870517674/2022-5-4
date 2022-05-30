---
title: Linux常用指令 2022_5_15 - 2022_5_18
---
### 1. 在CentsOS的Linux上`useradd jack`会在home目录创建一个Jack文件夹，也就是创建用户，useradd是创建用户命令

### 2. home文件夹是存放用户的文件夹，在Linux，一切皆文件

### 3. `userdel -r jack`是删除Jack用户也就是会把文件夹删除`userdel -r`是删除用户命令

### 4. `ifconfig`命令查看网络的ip地址

### 5. `reboot`，重启，我们在Windows使用Xshell7连接CentOS输入命令，虚拟机的CentOS会执行；其他任何命令都一样

### 6. vim，使用vim编辑器，只需要在命令行输入`vim xxx.xxx`，然后回车，然后输入i进入插入模式，可以开始写代码了。

### 7. 写完之后输入先点击`esc`，然后输入冒号进入命令行模式，`wq`，保存并退出，是一起输入的也就是:wq就行(`q`退出  `:q!`不保存退出)

### 8. 在进入vim后，在一般模式下(即非插入也非命令行，也就是刚开始的时候)输入`yy`是拷贝当前光标所在行，输入`p`是粘贴

### 9. `dd`删除当前行，可以数字dd，数字yy，比如`5dd`，`5yy`拷贝第五行，删除第五航这种操作

### 10. 查找，输入/然后输入需要查找的字符即可，比如`/hello`，在编辑模式下的的vim就行

### 11. 设置文件的行号，需要在命令行下，输入`:set nu`,冒号就是表示命令行

### 12. 去掉文件行号，输入:`set nonu`

### 13. 定位到vim文件末尾在正常模式输入`G`，文件首输入`gg`
 
### 14. 文件中撤销刚才的输入，一般模式下输入`u`。（强调一下，输入i就是插入模式，键盘的esc可以退出，就变成一般模式）

### 15. 光标定位:在一般模式下输入：`行号+shift+g`


插入模式就是在一般模式输入i就可以进入
一般模式就是刚开始的时候
命令行模式就是在一般模式输入:或/然后开始输入命令
### 16.关机&重启命令

`shutdown -h now` 立即关机
`shudown -h 1`   一分钟后关机
`shutdown -r now` 现在重新启动计算机
`halt`            关机，作用和上面一样
`reboot`          现在重新启动计算机
`sync`            把内存的数据同步到磁盘

### 17. 如果是非管理员账号，可以用"`su - 用户名`"切换管理员身份，比如“`su - root`”然后会显示一个密码，注意，你输入数字的过程是没有反馈的，不要管，直接输入，输入完回车就行，直接su也行

### 18. logout，注销账户，如果已经注销之前的账号，再次使用会退出系统，logout注销指令在图形界面运行级别无效，在运行级别3下有效，比如Xshell

### 19. 添加用户useradd 用户名，比如添加一个milan，是`useradd milan`，用户的家目录默认在home文件夹内，可以用`cd /home`然后ls查看

### 20. 添加用户指定位置：比如这样`useradd -d /home/test king` 创建了test目录用户名是king，test目录是king的家目录，而不是默认生成的

### 21. 给用户设置密码给milan设置密码为milan：`passwd milan`。注意输入密码是没有反馈的，输入完回车就有反馈了

### 22. `pwd`，返回当前所在目录

### 23. 删除用户：`userdel 用户名`

### 24. 删除用户及其家目录，`userdel -r 用户名`

### 25. 查询用户的信息，比如root 用户就`id root`

### 26. 再次强调一下“`su -用户名`”切换用户名，如果是高权限切换低权限不需要输入密码

### 27. 查看当前用户信息`who am I`
### 28. 用户组 类似与角色，系统可以对有共性/权限的多个用户进行统一的管理
新增用户组：`groupadd` 组名 删除组 `groupdel 组名`

### 29. 增加用户时直接加上组：useradd -g 用户组 用户名
    增加一个用户zwj，直接将他指定到wudang: 
`groupadd wudang` 
`useradd -g wudang zwj`
    可以用id查看用户所在的组
    如果创建用户的时候没有创建组，会自动创建名字和用户一样的组

### 30. 修改用户的组把zwj放入到mojiao组：先创建mojiao组`groupadd mojiao ` `usermod -g mojiao zwj`

### 31. 用户配置文件，在`/etc/passwd`文件下有，可以使用vim查看，每行的含义：用户名:口令:用户标识符:组标识号:注释性描述:主目录:登录Shell

### 32. 口令的配置文件，在`etc/shadow`。存放着登录名：加密口令：最后一次修改时间：最小时间间隔：最大时间间隔：警告时间：不活动时间：失效时间：标志

### 33. 组的配置文件，在`/etc/group`，使用vim /etc/group查看，每行含义：组名：组标识号：组内用户列表

### 34 .指定运行级别
0. :关机
1. :单用户    【找回丢失密码】
2. :多用户状态没有网络服务
3. :多用户状态有网络服务
4. :系统未使用保留给用户
5. :图形界面
6. :系统重启
常用运行级别是3和5，也可以默认运行级别
命令:`init 数字`比如`init 3`就是没有图形界面的有网络情况，命令行，还可以输入`init 5`回到之前状态
`systemctl get-default`查看当前的运行级别
`systemctl set-default multi-user.target`更改默认级别为3，也就是命令行了，输入用户和密码进入后，输入`init 5`回到图形界面即可

### 35. 找回root密码，看老韩文档

### 36. 虚拟机，**ctrl+alt**回到计算机，**ctrl+g**回到虚拟机

### 37. `help`输入help就能看见命令提示，英语不好百度

### 38. `pwd`显示当前的工作目录的绝对路径

### 39. `ls`显示当前目录文件

### 40. `clear`清除当前显示的数据

### 41. `man ls`显示ls的操作，相当于help的ls版本，告诉你ls如何使用，比如下面的

**`ls -a`列出所有文件，包括以 "." 开头的隐含文件，`ls -l`单列显示，用的比较多，并且可以组合输出，比如`ls -la`显示全部的包含.且单列打印**
**或者`ls -la\root`也就是显示root目录下的所有且单列，或者`ls -la\home`**

        -1,                                                --format=single-column
       一行输出一个文件（单列输出）。如标准输出不是到终端， 此选项就是缺省选项。

       -a, --all
              列出目录中所有文件，包括以“.”开头的文件。

       -b, --escape
              把文件名中不可输出的字符用反斜杠加字符编号(就象在                C
              语言里一样)的形式列出。

       -c, --time=ctime, --time=status
              按文件状态改变时间（i节点中的ctime）排序并输出目录内
              容。如采用长格式输出（选项“-l”），使用文件的状态改
              变时间取代文件修改时间。【译注：所谓文件状态改变（i节
              点中以ctime标志），既包括文件被修改，又包括文件属性（
              如所有者、组、链接数等等）的变化】

       -d, --directory
              将目录名象其它文件一样列出，而不是列出它们的内容。

       -f     不排序目录内容；按它们在磁盘上存储的顺序列出。同时启    动“     -a
              ”选项，如果在“   -f   ”之前存在“   -l   ”、“   -  -color  ”或“  -s
              ”，则禁止它们。

       -g 忽略，为兼容UNIX用。

       -i, --inode
              在每个文件左边打印 i 节点号（也叫文件序列号和索引号:  file  serial
              number and index number）。i节点号在每个特定的文件系统中是唯一的。

       -k, --kilobytes
              如列出文件大小，则以千字节KB为单位。

       -l, --format=long, --format=verbose
              除每个文件名外，增加显示文件类型、权限、硬链接数、所
              有者名、组名、大小（        byte        ）、及时间信息（如未指明是
              其它时间即指修改时间）。对于6个月以上的文件或超出未来            1
              小时的文件，时间信息中的时分将被年代取代。

              每个目录列出前，有一行“总块数”显示目录下全部文件所
              占的磁盘空间。块默认是   1024   字节；如果设置了   POSIXLY_CORRECT
              的环境变量，除非用“    -k     ”选项，则默认块大小是     512     字
              节。每一个硬链接都计入总块数（因此可能重复计数），这无
              疑是个缺点。

       列出的权限类似于以符号表示（文件）模式的规范。但是 ls
              在每套权限的第三个字符中结合了多位（     multiple     bits      ）
              的信息，如下：     s     如果设置了     setuid     位或     setgid
              位，而且也设置了相应的可执行位。 S 如果设置了 setuid  位或  setgid
              位，但是没有设置相应的可执行位。      t      如果设置了     sticky
              位，而且也设置了相应的可执行位。     T      如果设置了      sticky
              位，但是没有设置相应的可执行位。                                 x
              如果仅仅设置了可执行位而非以上四种情况。                         -
              其它情况（即可执行位未设置）。

       -m, --format=commas
              水平列出文件，每行尽可能多，相互用逗号和一个空格分隔。

       -n, --numeric-uid-gid
              列出数字化的 UID 和 GID 而不是用户名和组名。

       -o     以长格式列出目录内容，但是不显示组信息。等于使用“    --format=long
              --no-group ”选项。提供此选项是为了与其它版本的 ls 兼容。

       -p     在每个文件名后附上一个字符以说明该文件的类型。类似“ -F ”选项但是不
              标示可执行文件。

       -q, --hide-control-chars
              用问号代替文件名中非打印的字符。这是缺省选项。

       -r, --reverse
              逆序排列目录内容。

       -s, --size
              在每个文件名左侧输出该文件的大小，以                          1024
              字节的块为单位。如果设置了 POSIXLY_CORRECT 的环境变量，除非用“  -k
              ”选项，块大小是 512 字节。

       -t, --sort=time
              按文件最近修改时间（           i           节点中的          mtime
              ）而不是按文件名字典序排序，新文件 靠前。

       -u, --time=atime, --time=access, --time=use
              类似选项“  -t   ”，但是用文件最近访问时间（   i   节点中的   atime
              ）取代文件修
              改时间。如果使用长格式列出，打印的时间是最近访问时间。

       -w, --width cols
              假定屏幕宽度是              cols              （              cols
              以实际数字取代）列。如未用此选项，缺省值是这
              样获得的：如可能先尝试取自终端驱动，否则尝试取自环境变量   COLUMNS
              （如果设 置了的话），都不行则取 80 。

       -x, --format=across, --format=horizontal
              多列输出，横向排序。

       -A, --almost-all
              显示除 "." 和 ".." 外的所有文件。

       -B, --ignore-backups
              不输出以“ ~ ”结尾的备份文件，除非已经在命令行中给出。

       -C, --format=vertical
              多列输出，纵向排序。当标准输出是终端时这是缺省项。使用命令名   dir
              和 d 时， 则总是缺省的。

       -D, --dired
              当采用长格式（“   -l   ”选项）输出时，在主要输出后，额外打印一行：
              //DIRED// BEG1 END1 BEG2 END2 ...

       BEGn 和 ENDn 是无符号整数，记录每个文件名的起始、结束位置在输出中的位置（
              字节偏移量）。这使得                                         Emacs
              易于找到文件名，即使文件名包含空格或换行等非正
              常字符也无需特异的搜索。

       如果目录是递归列出的（“ -R ”选项），每个子目录后列出类似一行：
              //SUBDIRED// BEG1 END1 ...  【译注：我测试了 TurboLinux4.0 和 Red‐
              Hat6.1 ，发现它们都是在  “  //DIRED//  BEG1...  ”之后列出“  //SUB‐
              DIRED//  BEG1  ... ”，也即只有一个 而不是在每个子目录后都有。而且“
              //SUBDIRED// BEG1 ... ”列出的是各个子目 录名的偏移。】

       -F, --classify, --file-type
              在每个文件名后附上一个字符以说明该文件的类型。“                  *
              ”表示普通的可执行文件；  “  /  ”表示目录；“  @  ”表示符号链接；“ |
              ”表示FIFOs；“ = ”表示套接字 (sockets) ；什么也没有则表示普通文件。

       -G, --no-group
              以长格式列目录时不显示组信息。

       -I, --ignorepattern
              除非在命令行中给定，不要列出匹配  shell   文件名匹配式（   pattern
              ，不是指一般    表达式）的文件。在    shell    中，文件名以    "."
              起始的不与在文件名匹配式 (pattern) 开头的通配符匹配。

       -L, --dereference
              列出符号链接指向的文件的信息，而不是符号链接本身。

       -N, --literal
              不要用引号引起文件名。

       -Q, --quote-name
              用双引号引起文件名，非打印字符以 C 语言的方法表示。

       -R, --recursive
              递归列出全部目录的内容。

       -S, --sort=size
              按文件大小而不是字典序排序目录内容，大文件靠前。

       -T, --tabsize cols
              假定每个制表符宽度是    cols     。缺省为     8。为求效率，     ls
              可能在输出中使用制表符。 若 cols 为 0，则不使用制表符。

       -U, --sort=none
              不排序目录内容；按它们在磁盘上存储的顺序列出。（选项“  -U  ”和“ -f
              ”的不
              同是前者不启动或禁止相关的选项。）这在列很大的目录时特别有用，因为不
加排序
              能显著的加快速度。

       -X, --sort=extension
              按文件扩展名（由最后的                                         "."
              之后的字符组成）的字典序排序。没有扩展名的先列 出。

       --color[=when]
              指定是否使用颜色区别文件类别。环境变量                   LS_COLORS
              指定使用的颜色。如何设置   这个变量见   dircolors(1)    。    when
              可以被省略，或是以下几项之一：

       none 不使用颜色，这是缺省项。
              auto  仅当标准输出是终端时使用。 always 总是使用颜色。指定 --color
              而且省略 when 时就等同于 --color=always 。

       --full-time
              列出完整的时间，而不是使用标准的缩写。格式如同             date(1)
              的缺省格式；此格式        是不能改变的，但是你可以用        cut(1)
              取出其中的日期字串并将结果送至命令 “ date -d ”。

       输出的时间包括秒是非常有用的。（                                     Unix
       文件系统储存文件的时间信息精确到秒，
              因此这个选项已经给出了系统所知的全部信息。）例如，当你有一个 Make‐
              file 文件 不能恰当的生成文件时，这个选项会提供帮助。

GNU 标准选项
       --help 打印用法信息到标准输出并顺利退出。

       --version
              打印版本信息到标准输出并顺利退出。

       --     结束选项表。

### 42. cd指令，基本语法:`cd 参数` (功能描述:切换到指定目录)
`cd ~`或者`cd:`回到自己的家目录，比如是root用户`cd ~`到/root，再使用`pwd`看自己所在目录
`cd ..`回到当前目录的上一级目录,如果已经到了根目录，那么操作就无效
**案例**
1. :使用绝对路径切换到root目录,`cd/root`
2. :使用相对路径到/root目录,比如在`home/tom`，那么就`cd ../../root`
3. :表示回到当前目录的上一级目录,`cd ..`
4. :回到家目录,`cd ~`

### 43. mkdir指令
1. mkdir指令用于创建目录
    基本语法:`makdir 选项`要创建的目录
            `makdir -p`创建多级目录
    `-p`:创建多级目录
2. 应用实例
    1. 创建一个目录/home/dog `mkdir /home/dog`
    2. 创建多级目录/home/animal/tiger`mkdir -p /home/animal/tiger` 

### 44. rmdir指令
1. rmdir指令删除空目录
    基本语法: `rmdir 选项(要删除的目录)`

2. 应用实例:删除一个目录/home/dog`rmdir /home/dog`**rmdir指令不能删除有内容的目录**
    使用**rm -rf**可以解决上面的问题 比如删除一个非空的demo`rm -rf /home/demo`

### 45. touch指令
1. touch指令创建空文件
    基本语法:`touch 文件名称`
    应用实例:在/home目录下创建一个空文件hello.txt 先使用cd命令确保自己在home目录下，然后使用`touch hello.txt`

### 46. cp指令
1. cp指令拷贝文件到指定目录
    基本语法:`cp [选项] source dest`
    常用选项:`-r`递归复制整个文件夹
2. 应用实例
    1. 将/home/hello.txt拷贝到/home/bbb目录下
        `mkdir ddd` 先在home目录下创建add文件夹(确保自己在home目录下操作)
        `cp hello.txt ddd/`
    2. 递归复刻整个文件夹，举例，比如将/home/bbb整个目录 拷贝到/opt`cp -r /home/ddd/ /opt`
    3. 强制覆盖不提示的方法:`\cp`(强制覆盖是指已经有了相同的文件夹依旧拷贝，那么系统就会提示是否要覆盖，输入y就是强制覆盖)

### 47.rm指令
1. 说明:rm指令移除文件或目录
    基本语法`rm [选项]要删除的目录或文件夹`
2. 常用选项:
    1. -r:递归删除整个文件夹
    2. -f:强制删除不提示
3. 常用实例
    1. 将/home/hello.txt删除  `rm hello.txt`或`rm -f hello.txt` 第一个需要输入y确定 第二个则不需要 这两个的前提是先`cd /home`了，也可以使用绝对路径`rm /home/hello.txt`
    2. 递归删除整个文件夹/home/ddd  
        1. `rm -r /home/ddd`这种方式会一个一个提示你ddd文件夹内的东西是否要删除，得不停的输入y，
        2.  `rm -rf /home/ddd`*强制删除整个文件夹不提示，`-rf`就是`-r`和`-f`的组合的意思*

**/是根目录,在左边的时候，比如cd或者任何指令，如果要从根目录那么就cd /，如果是当前目录就不加/，最后的/加不加无所谓**
### 48. mv指令
1. 移动文件与目录或重命名
2. 基本语法:
    1. `mv a.txt b.txt`(功能描述:重命名)这只是打个比方，在同级目录下，这样就是把a重命名为b
    2. `mv 路径`(功能描述:移动文件)
3. 应用实例
    1. 将/home/cat.txt文件重新命名为pig.txt`mv cat.txt  pig.txt`
    2. 将/home/pig.txt文件移动到/root目录下`mv pig.txt /root`   相当于剪切
        补充一点，也可也移动并且重命名`mv pig.txt /root/cow.txt`
    3. 移动整个目录,比如将/opt/ddd移动到/home下`mv /opt/ddd/ /home` mv后跟要移动目录的路径 再跟目标目录的路径

### 49. cat指令
1. cat查看文件内容
2. 基本语法:`cat 要查看的文件`
3. 常用选项:`-n`显示行号
4. 实用案例
    1. /etc/profile 文件内容，并显示行号`cat -n /etc/profile`

**使用细节**cat只能浏览文件，而不能修改文件，为了浏览方便，一般会带上 **管道命令**|more `cat -n /etc/profile | more` 下面有more的单独使用和更加详细的说明

### 50. more指令
1. 基本语法:`more 要查看的文件路径`
    1. 空格     翻页
    2. Enter    翻一行
    3. q        离开more 不再显示文件内容
    4. Ctrl+F   向下滚动一屏
    5. Ctrl+B   返回上一屏
    6. =        输出当前的行号
    7. :f       输出文件名和当前行号

### 51. less指令
1. less指令用来分屏查看文件内容 它的功能与more指令类似 但是比more更加强大 支持各种显示终端 
    less指令在显示文件内容时 并不是一次将整个文件加载之后才显示，而是根据显示需要加载内容，对于显示大型文件具有较高的效率
2. 基本语法:`less 要查看的文件路径`
3. 操作说明
    1. 空白键   向下翻动一页
    2. pagedown 向下翻动一页
    3. pageup   向上翻动一页
    4. /字串    向下搜寻【字典】的功能:n:向下查找;N:向上查找
    5. ？字串   和上面一样
    6. q        离开less这个程序

### 52. echo指令
1. echo输出内容到控制台
2. 基本语法:`echo [选项] 输出内容`
3. 案例
    1. 使用echo指令输出环境变量，比如输出$PATH AME $`echo $HOSTNAME`
    2. 使用echo指令输出hello,word!`echo "hello,word"`

### 53. head指令
1. head用于显示文件的开头部分 默认情况下head指令显示文件的前10行内容
2. 基本语法:
    1. `head 文件`  
    2. `head -n 5 文件`(查看文件头5韩内容，5可以是任意行数)
3. 案例，查找/opt/1.txt文件的前3行内容`head -n 3 /opt/1.txt`

### 54. tail指令
1. tail用于输出文件尾部的内容，默认情况下tail指令显示文件的前10行内容
2. 基本语法
    1. `tail 文件`(查看文件尾10行内容)
    2. `tail -n 5 文件`(查看文件尾5行内容 5可以是任意行数)
    3. `tail -f 文件`(实时追踪该文件的所有更新)
3. 案例
    1. 查看/opt/1.txt文件的后5行代码`tail -n 5 /opt/1.txt`
    2. 实时监控1.txt 看看到文件有变化时，是否能看到，实时的追加日期`tail -f /opt/1.txt`输入**Ctrl+C**退出此模式

### 55. 文件目录类
1. `>指令`和`>>指令`
2. 基本语法
    1. `ls -l >文件`(列表的内容写入文件中(覆盖写))
    2. `ls -al >>文件`(列表的内容追加到文件的末尾)
    3. `cat 文件1 > 文件2`(将文件1的内容覆盖到文件2)
    4. `echo 内容 >> 文件`(追加)
3. 应用实例
    1. 将/home目录下的文件列表，写入到/home/info.txt中，覆盖写入 `ls -l /home > /home/info.txt` ==如果info.txt不存在,则会创建==
    2. 将当前日历信息 追加到/home/mycal文件中 ==如果mycal不存在会自动创建
       == `cal`==可以显示当前的日历信息，所以答案是`cal >>/home/mycal`

### 56. ln指令
1. 软链接也称为符号链接 类似于Windows里的快捷方式 主要存放了链接其他文件的路径
2. 基本语法:`ln -s[原文件][软链接名]`(给原文件创建一个软链接)
3. 应用案例
    1. 在/home目录下创建一个软连接 myroot 连接到/root`-s /root /home/myroot`
    2. 删除软连接myroot`rm /home/myroot`

### 57. history指令
1. 查看已经执行过历史命令，也可也执行历史命令
2. 基本语法:`history`(查看已经执行过的历史命令)
3. 应用实例
    1. 显示所有的历史命令`history`
    2. 显示最近使用过的10个指令`history 10`
    3. 执行历史编号为5的指令`history !5`

##  时间日期类
### 58. 显示当前日期
1. 基本语法
    1. `date`(显示当前时间)
    2. `date+%Y`(显示当前年份)
    3. `date+%m`(显示当前月份)
    4. `date+%d`(显示当前是哪一天)
2. 案例实例
    1. 显示当前时间信息     `date`
    2. 显示当前年月日       `date "+%Y-%m-%d"` 不加`-`也行，只是让我们看着好看一点而已
    3. 显示当前年月日时分秒 `date "+%Y-%m-%d %H:%M:%S"` 注意大小写
3. date指令设置日期
    1. 基本语法:`date -s 字符串时间`
    2. 应用实例:设置系统当前时间 比如设置成2020-11-03 11:22:22 `date -s "2020-11-03 20:01:10"`
### 59. cal指令
1. 查看日历指令cal
2. 基本语法`cal 选项`(如果不加选项 显示本月日历)
3. 应用实例
    1. 显示当前日历`cal`
    2. 显示2020年日历`cal 2020`

## 搜索查找类
### 60. file指令
1. file指令将从指定目录向下递归地遍历其各个子目录 将满足条件的文件或者目录显示在终端
2. 基本语法 `file [搜索范围] [选项]`
3. 选项说明:
    1. `-name<查询方式>`  (按照指定的文件名查找模式查找文件)
    2. `-user<用户名>`    (查找属于指定用户名的所有文件)
    3. `-size<文件大小>`  (按照指定的文件大小查找文件)
4. 应用实例:
    1. 按文件名:根据名称查找/home 目录下的hello.txt文件`find /home -name hello.txt`
    2. 按拥有者:查找/opt目录下 用户名称为root的文件`find /opt -user root`
    3. 查找整个Linux系统下大雨200M的文件(+n 大于 -n小于 n等于 什么都不写也是等于)`find / -size +200M`
        可以先cd到目录，然后使用`ls -lh`来查看文件大小 `h`的作用主要是把字节转换为我们的k，M这样的单位

### 61. locate指令
1. locate指令可以快速定位文件路径 locate指令利用实现建立的系统中所有文件名称及路径的locate数据库实现快速定位给定的文件 
    locate指令无需遍历整个文件系统 查询速度较快 为了保证查询结果的准确的 管理员必须定期更新locate时刻
2. 基本语法:`locate 搜索文件`
**特别说明 由于locate指令基于数据库进行查询 所以第一次运行前 必须使用`updatedb`指令创建locate数据库**
3. 应用实例:请使用locate指令快速定位hello.txt文件所在目录`locate hello.txt`

### 62.which指令
1. 可以查看摸个指令在哪个目录 比如ls在哪个目录`which ls`

### 63.grep指令和管道符号|
1. grep过滤查找 管道符| 表示将前一个命令的处理结果输出传递给后面的命令处理
2. 基本语法`grep [选项] 查找内容 源文件`
3. 常用选项: `-n` 显示匹配行及行号    `-i` 忽略字母大小写
3. 应用实例
    1. 在hello.txt文件中 查找yes所在行 并且显示行号
        写法1:`cat/home/hello.txt | grp -n "yes"`
        写法2:`grep -n "yes" /home/hello.txt`

## 压缩和解包类
### 64. gzip/gunzip指令
1. gzip用于压缩文件 guzip用于解压的
2. 基本语法:
    1. `gzip 文件`(压缩文件 只能将文件压缩为*.gz文件)
    2. `guzip 文件.gz`(解压缩文件命令)
3. 应用实例:
    1. gzip压缩 将/home下的hello.txt文件进行压缩`gzip /home/hello.txt`
    2. guzip压缩 将/home下的hello.txt.gz文件进行解压缩``

### 65. unzip的常用选项
1. `-d<目录>:指定解压后文件的存放目录`
2. 应用实例
    1. 讲/home下的所有文件压缩成myhome.zip`-r myhome.zip /home`
    2. 将myhome.zip解压到/opt/tmp目录下`unzip -d /opt/temp`

### 66. tar指令
1. tar指令是打包指令 最后打包后的文件是.tar.gz的文件
2. 基本语法:`tar [选项] XXX.tar.gz 打包的内容`(打包目录 压缩后的文件格式.tar.gz)
3. 选项说明
    1. -c   产生.tar打包文件
    2. -v   显示详细信息
    3. -f   指定压缩后的文件名
    4. -z   打包同时压缩
    5. -x   解包.tar
4. 应用实例:
    1. 压缩多个文件 将/home/pig.txt和/home/cat.txt压缩成pc.tart.gz`tar -zcvf pc.tar.gz /home/pig.txt /home/cat.txt`
    2. 将/home 的文件夹 压缩成 myhome.tar.gz`tar -cvf myhome.tar.gz /home`
    3. 将pc.tar.gz解压到当前目录`tar -zxvf pc.tar.gz`

## Linux组

### 67. Linux组的基本介绍
1. 在Linux中的每个用户必须属于一个组 不能独立于组外 在Linux中每个文件有所有者 所有组 所在组 其他组的概念
    1. 所有者
    2. 所在组
    3. 其他组
    4. 改变用户所在的组

### 68. 文件/目录 所有者
1. 一般为文件的创建者 谁创建了该文件 就自然成为该文件的所有者
2. 查看文件的所有者
    1. 指令:`ls -ahl`
    2. 应用实例 修改文件所有者 指令:`chown 用户名 文件名`
    3. 应用案例 要求root创建一个文件apple.txt 然后将其所有者修改成 tome`chown tom apple.txt`

### 69. 组的创建
1. 基本指令`groupadd 组名`
2. 应用实例
    1. 创建一个组 monster`groupadd monster`
    2. 创建一个用户 fox 并放到monster组中`useradd -g monster fox` 可以使用id命令查看用户所在组`id fox `

### 70. 文件/目录 所在组
1. 查看文件/目录所在组
2. 基本指令 `ls -ahl`
    1. 使用fox来创建一个文件 看看该文件属于哪个组 **因为前面我们把fox用户放在monster组中 所以创建的文件所在的组就是monster**
3. 应用实例
    1. 修改文件所在的组 基本指令 `chgrp 组名 文件名`
    2. 应用实例 使用root用户创建文件 orange.txt 看看当前这个文件属于哪个组 然后将这个文件所在组 修改到fruit组
        1. `groupadd fruit`(先创建组)
        2.  `touch orange.txt`(创建一个文件)
        3. 看看当前这个文件属于哪一个组-> root组
        4. `chgrp fruit orange.txt`(修改所在组)
**文件和目录都可以这样操作**

### 71. 其他组
1. 除文件的所有者和所在组的用户外 系统改变其他用户都是文件的其他组
#### 改变用户所在组
1. 在添加用户时 可以指定将该用户添加到组中 同样的用root的管理权限可以改变某个用户所在的组
2. 改变用户所在组
    1. `usermod -g 新组名 用户名`
    2. `usermod -d 目录名 改变该用户登录的初始目录`**用户需要有进入到新目录的权限**
3. 应用实例
    1. 将zwj这个用户从原来梭子啊的组 修改到wudang组`usermod -g wudang zwj`

## Linux权限

### 72. 权限的基本介绍
1. `ls -l`中显示的内容如下
    -rwxrw-r-- 1 root 1213 Feb 2 09:39 abc
    0-9位说明
    1. 第0位确定文件类型(d,-,l,c,b)
        -是普通文件
        l是链接 相当于Windows的快捷方式
        d是目录 相当于Windows的文件夹
        c是**字符设备**问价 鼠标 键盘
        b是块设备 比如硬盘
    2. 第1-3位确定所有者(该文件的所有者)拥有该文件的权限。 User
    3. 第4-6位确定所属组(同用户组的)拥有该文件的权限 --Group
    4. 第7-9位确定其他用户拥有该文件的权限 --Other

### 73.rwx权限详解 难点
1. rex作用到文件
    1. [r]代表可读(read):可以读取 查看
    2. [w]代表可写(write):可以修改 但是不代表可以删除该文件 删除一个文件的前提是对该文件所在的目录有写的权限 才能删除该文件
    3. [x]代表可执行(execute):可以被执行
2. rwx作用到目录
    1. [r]代表可读(read):可以读取 ls查看目录内容
    2. [w]代表可写(write):可以修改 对目录内创建+修改+重命名目录
    3. [x]代表可执行(execute):可以进入该目录

### 74. 文件及目录权限实际案例
1. ls -l中显示的内容如下
    1. **-rwxrw-r-- 1 root root 1213 Feb 09:39 abc**
    10个字符确定不同用户能对文件干什么
    第一个字符代表文件类型:- l d c b
    其余三个字符一组(rwx) 读(r)写(w)执行(x)
    第一组rwx:文件拥有者的权限是读、写和执行
    第二组rw-:与文件拥有者同一组的用户的权限是读、写 但是不能执行
    第三组r--:不与文件拥有者同组的其他用户的权限是读不能写和执行
    2. **可用数字表示位:r=4,w=2,x=1因此rwx=4+2+1=7**
    其他说明
    1           文件:硬链接或 目录:子目录数
    root        用户
    root        组
    1213        文件大小(字节) 如果是文件夹 显示4096字节
    Feb 2 09:39 最后修改日期
    abc         文件名

### 75. 权限修改-chmod
1. 基本说明:通过chmod指令可以修改文件或者目录的权限
2. 第一种方式:`x - =`变更权限
    u:所有者 g:所有组 o:其他人 a:所有人(u,g,o的总和)
    1. chmod u=rwx,g=rx,o=x 文件/目录名
    2. chmod o+w 文件/目录名
    3. chmod a-x 文件/目录名
    案例演示
    1. 给abc文件 的所有者读写执行的权限 给所在组执行权限 给它组读执行权限
    `chmod u=rwx,g=rx,p=rx abc`
    2. 给abc文件的所有者除去执行的权限 增加组写的权限
    `chmod u-x,g+w abc`
    3. 给abc文件的所有用户添加读的权限
    `chmod a+r abc`
3. 第二种方式:通过数字变更权限
    r=4 w=2 x=1 rxw=4+2+1=7
    chmod u=rwx g=rx o=x 文件目录名
    相当于chmod 751文件目录名
    **案例演示**
    要求:将/home/abc.txt 文件的权限修改成 rwxr-xr-x 使用数字的方式实现:
    `chmod 755/home/abc.txt`

### 76. 修改文件所有者-chown
1. 基本介绍
    1. `chown newowner 文件/目录 改变所有者`
    2. `chown newowner:newgroup 文件/目录 改变所有者和所在组`
    ==-R==  如果是目录 则让其下所有子文件夹或目录递归生效
2. 案例演示:请将/home/abc.txt文件的所有者改成tom
`chown tom /home/abc.txt`
3. 请将/home/test目录下所有文件和目录的所有者都改成tom
`chown -R tom /home/test`

### 77. 最佳实践-警察和土匪游戏
police jerry:警察
xh xq:土匪
1. 创建组
    `groupadd police`  `groupadd bandit`
2. 创建用户
    `useradd -g police jack` `useradd -g police jerry`
    `useradd -g bandit xh`   `useradd -g bandit xq`
3. **jack**创建一个文件 自己可以读写 本组人可以读 其他组没人任何权限
    首先jack登录 `vim jack.txt` `chmod 640 jack.txt0`
4. **jack**修改该文件 让其他组人可以读 本组人可以读写
`chmod o=r,g=r jack.txt`
5. **xh**投靠 警察 看看是否可以读写
`usermod -g police xh`

### 88. 权限管理练习2   P49
1.    groupadd sx
2.    groupadd yg
3.    useradd ts
4.    useradd wk
5.    useradd bj
6.    useradd ss
7.    passwd ts
8.    passwd wk
9.    passwd bj
10.   passwd ss

### 88.在Linux下编写执行C/C++代码
1. 如何编写创建就不说了 如果编写好了源代码 
2. 输入`gcc 文件名`就编译完成
3. 默认是a.out 只需要输入`./a.out就能编译完成`

### 99.crond任务调度
1. 基本语法&常用选项
    1. ` crontab 选项`
    2. 常用选项
        1. `-e` 编辑crontab定时任务
        2. `-l` 查询crontab任务
        3. `-r` 删除当前用户所有的crontab任务
2. 快速入门
    1. 设置任务调度文件:`etc/crontab`
    2. 设置个人任务调度。执行`crontab -e命令`
    3. 接着输入任务到调度文件 比如:`*/1 * * * *ls -l/etc/ >tmp/to.txt`
        意思是说每个小时的每分钟执行`ls -l/etc/>/tmp/to.txt`
3. 参数细节说明 **五个占位符的说明**
    1. 一小时当中的第几分钟 范围:`0-59`
    2. 一天中的第几小时     范围:`0-23`
    3. 一个月当中的第几天   范围:`1-31`
    4. 一年当中的第几个月   范围:`1-12`
    5. 一周当中的星期几     范围:`0-7(0和7都代表星期日)`
4. 特殊符号的说明
    1. `*`代表任何时间  比如第一个`*`就代表一小时中每分钟都执行一次的意思
    2. `,`代表不连续的时间 比如`0 8,12,16 * * *命令` 代表在周一到周六的凌晨五点0分执行命令
    3. `-`代表连续的时间范围 比如`0.5 * * 1-6命令` 代表在周一到周六的凌晨5点0分执行命令
    4. `*/n`代表每隔多久执行一次 比如`*/10 * * * * 命令`代表每隔十分钟就执行
5. crond相关指令
    1. `conrtab -r`终止任务调度
    2. `crontab -l`列出当前有哪些任务调度
    3. `service crond restart`重启任务调度

### 100.crond案例
1. 对于shell脚本 我们写了一个例子 创建一个脚本文件**my.sh**然后写入
    `date >> /home/mycal`
    `cal >> /home/mycal`
    也就是追加时间和日期到mycal文件 如果mycal不存在会自己创建 默认追加 
    我们使用`./my.sh`也就是./文件名 和运行c/c++程序一样
2. 把上面的脚本每隔一分钟执行一遍
    我们先`crontab u+x -e`创建定时任务 这里的u和x是给my.sh增加执行权限
    然后写入`*/1 * * * * /home/my.sh`也就是每隔一分钟执行一下先前创建的脚本
3. 每天凌晨2:00将mysql数据库testdb，备份到文件中 提示:
    指令为**mysqldump -u root -p密码 数据库>> /home/db.bak** 步骤如下
    1. `crontab -e`
    2. `0 2 * * * mysqlump -u root -p1234 db01 > /home/db.bak`

### 101.at定时任务
1. at命令是一次性定时计划任务 at的守护进程atd会以后台模式运行 检查作业队列来运行
2. 默认情况下 atd守护进程每60秒检查作业队列 有作业时 会检查作业运行时间 如果时间与当前时间匹配 则运行此作业
3. at命令是一次性定时计划任务 执行完一个任务后不再执行此任务了
4. 在使用at命令的时候 一定要保证atd进程的启动 可以使用相关指令来查看
    `ps -ef`指令可以看到当前进程 也可以过滤 如下
    `ps -ef | grep atd` 查看atd进程是否正在运行

5. at命令格式
    1. `at 选项 时间`
    2. `Ctrl+D 结束at命令的输入`
    3. 选项的含义*百度吧*
        1. 
    4. 应用实例
        1. 2天后的下午5点执行/bin/ls/home`at 5pm + 2 days`回车后输入 `/bind/ls /home` 然后键盘两次**Ctrl+D**退出
        2. atq命令来查看系统中没有执行的工作任务`atq` 刚好可以用来查看先前的是否成功
        3. 明天17点钟 输出时间到指定文件内 比如/root/date100.log `/bind/ls /home`回车`/root/date100.log` 键盘两次**Ctrl+D**  
        4. 2分钟后 输出时间到指定文件内 比如/root/date200.log`at now + 2 minutes`回车`date > /root/date100.log`键盘两次**Ctrl+D**
            两分钟后可以`cd /root` 然后`cat date100.log`查看是否成功 同时运行完毕后 使用`atq`查看 正常来说运行完之后就不会再显示了
        5. 删除已经设置好的任务 atrm 编号 这个很简单 比如`atrm 1`
        6. 当然除了命令我们也可以执行脚本 举个例子两分钟后执行我再root目录下的脚本`at 5pm + 2 days`回车后输入`/root/my.sh`键盘两次**Ctrl+D**    如果失败先确保守护进程是否开启同时脚本是否有足够的权限
## 102.Linux分区
1. 原理介绍
    1. Linux来说无论有几个分区 分给哪一目录使用 它归根结底就只有一个根目录 一个独立且唯一的文件结构 Linux中每个分区都是用来组成整个文件系统的一部分
    2. Linux采用了一种叫**载入**的处理方法 它的整个文件系统中包含了一整套的文件和目录 且将一个分区和一个目录联系在一起 这时候要载入的一个分区将使他的存储空间在下一个目录下获得
    3. 查看所有设备的挂载情况 命令`lsblk`或`lsblk -f`   
    **更加详细的看韩顺平PDF**

### 102.1 Linux挂载的经典案例
1. 说明:下面我们以增加一块硬盘为例来熟悉下磁盘的相关指令和深入理解磁盘分区 挂载 卸载的概念
2. 如何增加一块硬盘
    1. 虚拟机添加硬盘
    2. 分区
    3. 格式化
    4. 挂载 
        虚拟机增加硬盘步骤4
        挂载 将一个分区与一个目录联系起来
        **mount 设备名称 挂载目录**
        例如:`mount /dev/sdb1 /newdisk`
        **umount 设备名称 或者 挂载目录**
        例如:`umount /dev/sdb1 或者 umount /newdisk`
            **挂载是`mount` 卸载是`umount`**
        ***命令行挂载 重启后会失效***

    5. 设置可以启动挂载
        永久挂载 通过修改/etc/fstab实现挂载
        添加完成后 执行mount -a即刻生效

### 103.磁盘情况查询
1. 基本语法`df -h`
2. 查询指定目录的磁盘占用情况`df -h 目录`
    1. `-s`指定目录占用大小汇总
    2. `-h`带计量单位
    3. `-a`含文件
    4. `--max-depth=1` 子目录深度
    5. `-c`列出明细的同时增加汇总值
3. 应用实例 查询/opt 目录的磁盘占用情况 深度为1
    `du -h --max-depth=1  /opt`
    如果想要显示含文件的大小可以组合参数a`du -ha --max-depth=1  /opt`
    如果还想显示总共的大小 还可以组合c`du -hac --max-depth=1  /opt`

### 104.磁盘情况-工作实用指令
1. 统计/opt文件夹下文件的个数`ls -l /opt | grep "^-" | wc -l` 这里的wc是数单词的 经过前面grep的过滤 正则表达式后 单词数量也就是文件数量
2. 统计/opt文件夹下目录的个数`ls -l /opt | grep "^d" | wc -l`目录都是以d结尾的 正则^d可以匹配
3. 统计/opt文件夹下文件的个数 包括子文件夹里的`ls -lR /opt | grep "^." | wc -l`
4. 统计/opt文件夹下目录的个数 包括文件夹里的`ls -lR /opt | grep "^d" | wc -l`   这两个都是只是把`ls -l`改成`ls -lR`
5. 以树状显示目录结构tree目录 **如果没有tree 使用`yum install tree`安装**   安装好后输入`tree /opt`即可