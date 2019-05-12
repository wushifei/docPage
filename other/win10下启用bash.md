# win10启用Linux Bash环境
> date:2019.05.12

1.首先启用：适用于Linux的Windows子系统（Beta）
打开控制面板->程序和功能->启用或关闭Windows功能，找到适用于Linux的Windows子系统（Beta），勾选上点确定，然后会让重启，选择重启。 
![1](/docPage/otherImgs/win-bash-1.png)

2.打开bash.exe进入cmd模式
在左下角搜索bash： 
![1](/docPage/otherImgs/win-bash-2.png)

点进去发现闪退 
首先：我们先进入cmd环境下，然后右击左上角，点属性。 
![1](/docPage/otherImgs/win-bash-3.png)

进去后检查使用旧版本控制有没有被勾选上，让其保持不被选中。 
![1](/docPage/otherImgs/win-bash-4.png)

然后再次搜索bash，点击后又是闪退。

然后从命令行模式打开windows\system32\bash.exe，给出了打不开的原因： 
![1](/docPage/otherImgs/win-bash-5.png)    

3.打开开发者模式
在设置->更新和安全->针对开发者。 
![1](/docPage/otherImgs/win-bash-6.png)    

打开后，我们再次打开，会提示安装Ubuntu，我们输入y，回车。
![1](/docPage/otherImgs/win-bash-7.png)    
若无法下载，在Microsoft store中搜索Linux，随便下载一个，并设置username&password

下载完成后，基本也就完成了，大家可以输几条命令试试。



// username：wushifei，password：921009