﻿# Kosmos安装指南
  本文（和文末链接中的文章）遵循MIT协议发布。你可以自由转载，修改本文，甚至用于商业用途————只需保留本声明即可。
  
  本文中提及的一切代码和二进制文件的所有权利均由对应作者拥有。

  许多switch自制玩家们偏爱免费的“大气层”自制系统，却苦于网络上的教程大都支离破碎，甚至显得有些过时，而不得不花费高额的成本转向SX系列产品。因此，有必要提供一份比较不易过时的教程。

  <del>本文基于KosmosV16.1编写，该版本基于Atmosphere0.12.0整合，使用hekate注入系统。为了完全发挥新版Kosmos的功能，需要9.0以上版本的Switch系统。
  
  Kosmos已经停止了开发，本文仅具有有限的参考价值。
  
  修订日期：2021.1.3

## 更新说明
	
  **Kosmos已经停止开发了，但你依然可以在本文中找到Deepsea的仓库获取整合包。**
  
  **教程本身是通用的，不必担心。**

  **相对于V15.6，V16.1主要**

  1.重做了整个Hekate/Nyx模块。你可以在Hekate/Nyx界面下将switch插入电脑，让电脑直接读取TF卡内的内容————就像用安卓手机一样。使用时需要在Nyx界面下手动启动USB Mass Storage——SD Card选项。
  
  2.新制作的文件形式的虚拟系统将使用FastFS文件格式，使用体验和分区形式的虚拟系统一样快。
  
  3.修复了使用9.0以下版本系统出现的bug————如果你使用9.0以下的系统，Kosmos会关闭很多新功能来保持兼容性。

  **KosmosV15.3及更低版本的用户必须删除旧自制文件**（比如，你可以删去除了Nintendo,emummc和Backup文件夹以外的所有内容）后安装。删除这些文件不会影响你已经安装的游戏和存档。
  
  使用基于LayeredFS的各种系统补丁（如系统主题，Homebrew引导补丁等）的用户建议删除atmosphere/titles和atmosphere/contents内的相关内容后安装。


  你可能会想尝试不删除旧自制文件，直接覆盖新自制包。但这会导致无法正常启动自制系统（这一般是过时的系统组件（modules）引起的），结果如下图所示。
  
![不删后果自负](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/2168-0002.jpg "不删后果自负")

# 综述

  “大气层”自制系统是SciresM主导的一个名为”Atmosphere”的项目，不过因为SciresM是一名坚定的正版支持者，原版的Atmosphere是不能直接用于玩盗版游戏的。实际上，我们所用的“大气层”都是其他人自行整合修改的。大部分整合包使用自制的payload，额外加载了SigPatch和其他一些组件，以允许你玩盗版游戏。

  其中最著名的一个版本就是使用hekate引导的Kosmos整合包。

## 准备工作
  在准备安装switch自制系统之前，确保你拥有一台具有RCM漏洞的switch，一张64G或者更大的TF卡，一个短接器，一条type-c数据线，一台电脑，一个读卡器。

### RCM漏洞

  2018年6月份之前生产的Switch具有RCM漏洞。**因此，由腾讯代理，于中国大陆发售的国行switch不在本文讨论范围之内。**

对于没有RCM漏洞的switch，如果系统版本在4.1或4.1以下，而且从未连过wifi，亦可使用自制系统。这部分用户请关闭本文，参照两个豆饭的帖子操作。如果你想使用未来的软破，不要使用官方升级升级最新系统（只有具备RCM漏洞的switch才能使用最新自制系统），离线升级用户也不要关闭autorcm。

  你可以根据序列号来确认switch是否具备rcm漏洞：

以XAW1开头的机型：

	XAW10078XXX和更小的序列号支持破解。
	XAW10079XXX可能可以破解。
	XAW1010XXX和更大的序列号不能破解。

以XAW4开头的机型：

	XAW40011XXX和更小的序列号支持破解。
	XAW40012XXX可能可以破解。
	XAW40013XXX和更大的序列号不能破解。

以XAW7开头的机型：

	XAW700178X和更小的序列号支持破解。
	XAW700179X可能可以破解。
	XAW70019X和更大的序列号不能破解。

以XAJ1开头的机型：

	XAJ1001XX和更小的序列号支持破解。
	XAJ1002XX可能可以破解。
	XAJ10031XX和更大的序列号不能破解。

以XAJ4开头的机型：

	XAJ40050X和更小的序列号支持破解。
	XAJ40051X可能可以破解。
	XAJ4006XX和更大的序列号不能破解。

以XAJ7开头的机型：

	XAJ70042X和更小的序列号支持破解。
	XAJ70043X可能可以破解。
	XAJ70044X和更大的序列号不能破解。

### 短接器

  短接器的目的是将switch机身右侧手柄卡槽内的Pin10与GND短接，让Tegra X1处理器在开机时进入RCM模式。

  你可以在淘宝上搜索“switch短接器”,用十块钱买到一个看上去相当不错的短接器。

  当然，你也可以自行制作短接器。锡纸短接法是目前比较流行的自制短接器方法，相信你一定能轻易百度到它的做法。由于自制短接器一般比较粗糙，如果你使用自制短接器，请尽量避免粗暴操作，以保护你的机身金手指。

  至于各种比较昂贵的“大气层U盘”或者“大气层注入器”，它们并不是switch破解的必备产品，你可以自行选择是否购买。
  
### switch的exFAT驱动

  exFAT文件系统支持超过4GB的大型游戏安装包，在TF卡上的读写速度也较快，非常实用。因此你现在能够购买到的大容量tf卡，出厂时均为exFAT格式。

  但是，switch出厂时，不具备读写exFAT格式TF卡的功能，该功能是任天堂向微软公司付费购买并通过系统更新提供给你的。有趣的是：在不插TF卡时，系统更新是不会为你安装exFAT驱动的。所以不论你的switch系统版本如何，只要你之前从未使用过TF卡，就一定要进行exFAT驱动检测。

  如果你第一次在switch上使用TF卡，为了确保你的switch具有exFAT驱动，最简单的检测方法是：在正版系统下插入TF卡开机。

  如果在正版系统下，插入TF卡后，switch一开机就提示：需要进行系统更新方能使用TF卡，则证明你缺少exFAT驱动。

  如果没有这样的提示，那么你的switch具备exFAT驱动，你可以跳过本小节了。

![该界面表示你缺少exfat驱动](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/need-to-update.jpg "该界面表示你缺少exfat驱动")

  在这一界面下，你固然可以直接点击"System Update"，更新到最新系统以获得exFat驱动。**但是，最新的系统有时不支持破解，因此这不是一个很好的方法。**

  如果你不想联网更新，则可以点击“Later”并关机。一种安全的安装exFAT驱动的方法是：通过离线更新的方法来获得exFAT驱动，从而避免联网。为了实现这种完美而复杂的方法，需要进行下面的三步操作：

	1：使用电脑将TF卡格式化成FAT32格式（如果不能格式化为FAT32格式，可以使用小一些（大于512MB即可）的TF卡，或者使用第三方格式化软件（如diskgenius）），之后跳过本小节，继续按本文所述的方法完成全套破解流程。

  如果你使用FAT32格式的TF卡破解，当然就不需要exFAT驱动了。但此时TF卡不能存放大于4G的nsp游戏安装包，因此在安装游戏时会有不少限制。所以，我们还需要执行下述两步操作。

	2：翻阅本文末尾的“离线免熔断刷入Switch系统”，按照教程刷一次机（版本号可变大，也可以不变，由您自行决定）。该操作可以把打包在系统更新内的exFAT驱动装入游戏主机内。
	3：使用电脑将TF卡格式化成exFAT，再次按本文的方法破解。该操作是为了将exFAT驱动的优势利用起来。

  如果你已经能在正版系统下使用exFAT格式的TF卡，则不需要担心这类问题。

## 下载必备软件

### Kosmos整合包

很遗憾，Kosmos已经停止开发了，不过你可以在Deepsea下载Hekate+Atmosphere整合包，获得类似Kosmos的体验。

对于普通用户而言，你可以在[Deepsea](https://github.com/Team-Neptune/DeepSea "Deepsea")这个仓库上下载整合包。该网站提供的整合包不含ES/FS/ACID补丁，不支持盗版游戏。目前[这个仓库](https://github.com/ITotalJustice/patches/releases/ "patches")提供了ES/FS/ACID补丁的功能，可以在此下载hekate版本。但这可能会导致ban机。请自行抉择。

使用ES/FS/ACID补丁可能会违反多条法律。

### TegraRCMGUI

  为了启动破解系统，你需要在 [TegraRcmGUI](https://github.com/eliboa/TegraRcmGUI/releases "TegraRcmGUI")这个网站上下载最新版本的[TegraRcmGUI_v2.6_portable.zip](https://github.com/eliboa/TegraRcmGUI/releases/download/2.6/TegraRcmGUI_v2.6_portable.zip "TegraRcmGUI_v2.6_portable.zip")

  如果你购买了大气层u盘，可以用大气层u盘替代这个程序。每种大气层u盘的操作方法均不相同，但原理都是将对应的payload注入到switch中，详情请咨询卖你u盘的店主。你可是交了税的，他们必须教你。

## 让我们开始吧

### 准备TF卡文件
  还记得刚刚你下载的Deepsea压缩包吧。你应该把里面的文件放入TF卡内。

  请使用Windows电脑打开这个压缩包，把压缩包目录下的所有文件拖入TF卡根目录（不要使用手机，安卓平板，或者MacOS电脑，这些操作系统对exFat文件系统的使用方法常常和ns不兼容，因而只能用于传输游戏，不能用于传输破解文件。）如果你的操作是正确的，当你打开TF卡后，应当能直接看到hbmenu.nro这个文件。

  另外，在压缩包中的“payloads”目录下找到hekate_ctcaer_x.y.z.bin，将文件移动到你的电脑上备用。这个文件就是其他教程中可能提到的payload.bin。  
  
  **如果你还下载了hekate版本的patches，你可以将该其解压后，将得到的的两个文件夹与tf卡内的同名文件夹合并。**
 
  **之后，修改/bootloader/hekate_ipl.ini，在前两次出现的fss0=atmosphere/fusee-secondary.bin下方各添加一行kip1patch=nosigchk**
 
  然后，将switch彻底关机（长按电源键8秒，switch将跳出关机菜单，选择power options-turn off），将TF卡插入你的switch。

  到此为止，你的switch已经准备就绪了。

### 启动破解系统
  接下来，我们讨论如何进入破解系统。

  如果你第一次操作，需要首先在你的私人电脑（不要使用网吧电脑，它们常常不能安装驱动）上解压TegraRcmGUI。你应当能看到一个名为apx_driver的文件夹，打开它。如果你的电脑运行着X64系统（大部分电脑都是这样的），双击InstallDriver，安装Switch RCM模式驱动。

  如果你的电脑已经具有了Switch RCM模式驱动，则可以运行TegraRcmGUI，点击Select Payload输入框右边的文件夹图标，打开刚刚预先准备的payload文件（比如hekate_ctcaer_x.y.z.bin）。

  卸下你的switch右joycon，将你的短接器插入switch右侧手柄导轨内，按住switch的音量键“+”，之后短按一次switch电源键。如果短接成功，switch看上去应当毫无变化。如果switch不幸开机了，请重试一次，直到成功为止。

  用type-c数据线链接你的switch和电脑，点击TegraRcmGUI上的Inject payload。

  如果你发现switch启动了，并显示了一些和正版系统不同的东西，你就可以拔去数据线和短接器，进入下一节了。

  如果点击按钮后，此时你的switch毫无变化，但电脑软件中的switch图标变绿了，很可能是因为你的switch没有RCM漏洞，暂不支持破解。

  **下一节非常重要。务必仔细阅读，不要跳过任何一步。**

### 配置你的破解系统
  如果你注入了Hekate，首先，你会看到一个图形界面菜单。
![漂亮的nyx界面](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/hekate-mainpage.jpg "漂亮的nyx界面")
  在该菜单下，你可以使用触摸屏进行所有操作。

  如果你第一次破解，那么，在进入破解系统之前，进行一次全盘备份有很多好处。比如，未来你可以用它修复switch的系统故障，或者用于“洗白”。

  我建议你选择Tools——Backup——eMMC boot0&boot1和Tools——Backup——eMMC raw GPP来进行一次全盘备份，耗时取决于你的TF卡性能，一般在0.5-2小时之间。

  建议TF卡预留33GB空间。

![点击屏幕上方的tools，再点击backup emmc](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/backup-mainpage.jpg "点击屏幕上方的tools，再点击backup emmc")
点击屏幕上方的tools，再点击backup emmc。

![选择一个备份选项，建议依次选择左边两项](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/choose-what-tobackup.jpg "选择一个备份选项，建议依次选择左边两项")
选择一个备份选项，建议依次选择左边两项。

![耐心等待备份完成，最后点击右上角close即可。](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/backup-nand.jpg "耐心等待备份完成，最后点击右上角close即可。")
耐心等待备份完成，最后点击右上角close即可。

  当你备份完成后，TF卡内会出现一个backup文件夹。你可以把它移动到你的电脑上，妥善保存，之后就可以删去TF卡上的备份文件了。这一备份是在进入破解系统前完成的，因此你可以放心地使用它。

  然后，建议你现在立刻制作一个虚拟系统（双系统）。如果你拥有了虚拟系统，那么你的破解行为均可在虚拟系统里完成，对真实的系统不造成影响，从而不容易因为操作不当而损坏switch。你可以参考：

[Atmosphere的虚拟系统配置](https://www.jianshu.com/p/d07b2bd992e5 "Atmosphere的虚拟系统配置")
  
  制作虚拟系统也需要花费约0.5-2小时。如果你已经拥有了系统备份，那么不花费时间制作虚拟系统也没有大碍。

  如果你已经完成了你的备份，制作完了虚拟系统（或者你根本不想备份/制作虚拟系统），那么：

![点击Launch](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/hekate-mainpage.jpg "点击Launch")
  点击Launch。

![点击CFW](https://github.com/ln93/kosmos_chs_tutorial/raw/master/imgs/hekate-launch.jpg "点击CFW")
  点击CFW。

  选择Launch。如果你做了虚拟系统，选择CFW(EMUNAND)可以进入虚拟破解系统，选择CFW(SYSNAND)可以进入真实破解系统；如果你没有做虚拟系统，选择CFW(SYSNAND)或CFW(EMUNAND)均只能进入真实破解系统。如果在点击CFW后发现Switch黑屏无法启动，建议回去重新阅读关于exFAT驱动的说明。

### 其他一些可能有用的说明
在该系统下，你的汉化补丁和mod放在atmosphere/contents文件夹内。

如果你使用Mac OS X破解，可以用hekate修复OS X造成的奇怪问题。

Mac用户在用Mac破解后，第一次开机时，选择Tools-Unset archive bit(switch folder)，耐心等待至绿字出现，按任意键返回即可。

## 我能开始玩了吗
### 保持断网
  在破解系统下，建议你保持断网状态。另外，打开飞行模式并不能保证你断网，因此建议你删除机内的所有wifi信息。否则，你的机子有可能被ban。另外，任天堂会疯狂向你推送升级信息，导致你打开各种游戏都会看到“游戏需要更新”的通知——十分烦人。

  如果你自认为是一个高级玩家，不希望完全断网，你可以用“90DNS”来屏蔽任天堂服务器(并不太可靠)。
  在WIFI设置中：

	将'Primary DNS' 设为 '163.172.141.219'
	将'Secondary DNS' 设为 '45.248.48.62'

  即可。

### 安装游戏
  待更新。
  
### 玩游戏
  建议你使用本地账户玩游戏，不要使用在线账户。一些长期联网的骨灰级破解玩家表示，使用本地账户玩nsp游戏可以有效降低被ban的概率。但一些新游戏会强制要求你使用在线账户游戏。

  对于SXOS/PRO用户的XCI游戏而言，本地账户不是必须的。但是如果你玩的游戏含有nsp DLC或者升级补丁，依然建议你使用本地账户。

## 其它一些有用的东西
  如果你喜欢本文，并且希望加入有趣的原神交流群，[欢迎加入原神交友群](https://jq.qq.com/?_wv=1027&k=qfu9Fe8l "欢迎加入原神交友群")。大多数情况下，群内的聊天主题和switch没什么关联。
  
  如果你对更个性化的修改感兴趣，可以参考：

  [利用手机代替电脑，启动switch自制系统](https://www.jianshu.com/p/0d865d92c7b0 "利用手机代替电脑，启动switch自制系统")

  [离线安装Switch系统](https://www.jianshu.com/p/6d5ba4be6cd8 "离线安装Switch系统")

  [使用Hekate恢复Rawnand备份](https://www.jianshu.com/p/7bf0d82576c0 "使用Hekate恢复Rawnand备份")


### 一些进阶内容：

  [制作和安装Switch主题](https://www.jianshu.com/p/62a8670252d7 "制作和安装Switch主题")

  [Atmosphere的虚拟系统配置](https://www.jianshu.com/p/d07b2bd992e5 "Atmosphere的虚拟系统配置")

  [基于sys-clk配置switch超频](https://www.jianshu.com/p/38c25923867a "基于sys-clk配置switch超频")

  [在Switch上运行ubuntu 18.04 L4T](https://www.jianshu.com/p/89df303b3384 "在Switch上运行ubuntu 18.04 L4T")
