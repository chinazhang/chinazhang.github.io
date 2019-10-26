Title: About Me
Date: 2019-10-07

# 备注几个十一期间浏览的网站

新增语音识别博主文章链接  http://pelhans.com/ https://blog.ailemon.me/2017/02/17/how-to-collect-data-for-machine-learning/  

免费的语音数据集  http://www.openslr.org/index.html   https://github.com/awesomedata

新增对撞机开放数据链接   http://opendata.cern.ch/docs/about-cms

# 设置atom相关命令备注

newchange "use git pull https://github.com/chinazhang/chinazhang.github.io.git" get Atom support

## 使用GitHub+Pelican搭建博客，并使用Atom作为编辑器的一些tips

Pelican 搭建博客后，GitHub上的master分支为网页文件，source分支为生成master分支内容的源代码。
因而Atom中我需要建立两个项目，一个与master分支同步，一个与source分支同步。

- 先与source分支同步，因为source使用命令 make html 运行后生成的网页文件是放在source里的output文件夹中的。而我需要先从GitHub上把source分支拉取下来，才能修改markdown文件，进而使用make html命令生成output中可以发布的网页文件。

- 使用如下命令拉取source分支的代码

```
git init
git remote add origin https://github.com/chinazhang/chinazhang.github.io.git
git pull origin source
```

- 进入output文件夹中，使用如下命令拉取master分支（猜测不拉也可以，等再source中make html后，再在这个文件夹里面强制push就可以了）

```
git init
git remote add origin https://github.com/chinazhang/chinazhang.github.io.git
git pull origin master
```

- 进入上一级文件夹，使用如下命令，新建source分支，切换到source分支

```
git branch source
git checkout source
```

至此，Atom中的source文件夹中同步就变成source分支同步了，而output文件夹仍然为master同步。完成了Atom的配置

make html需要到output的上一级文件夹里用git的bash窗口敲该命令，完成后到Atom里进行上传代码

## Pelican 备注

在content下面创建pages文件夹，并放一个md文件进去，就会在博客主页上多一个标签页。其他的准备学习下下面的官方手册

[Pelican官方手册链接](http://docs.getpelican.com/en/stable/)

## git 命令备注


- 删除GitHub上的某个文件夹

```
git rm -r --cached Photo 删除Photo文件夹
git commit -m '删除了Photo文件夹t'  提交,添加操作说明
git push -u origin master 将本次更改更新到GitHub项目上去
```

- 拉取GitHub的master或者source分支

```
git pull origin master
git pull origin source
```

## 其他备注

树莓派本地IP 192.168.137.102
mac account： zgw0254@icloud.com

# mac降版本安装

1、制作USB镜像命令

high sierra

```
sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia –-volume /Volumes/Sierra –-applicationpath /Applications/Install\ macOS\ High\ Sierra.app –-nointeraction
```

Catalina

```
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --nointeraction
```

   * If you want to be asked for confirmation before erasing the drive, remove “–-nointeraction” from the command.
   * Older versions of macOS used an “-–applicationpath” flag in this command, but this is now deprecated and will cause an error if used. Use the command above, instead of updating the command mentioned in guides which were written for previous versions of macOS



2、关机。开机时长按option键

3、Mojave 降级需要格式化

先在磁盘工具左上选择显示所有设备。
然后选择apple SSD 磁盘，抹除选项中名称为 Macintosh HD ，格式选 MAC OS Extened(journaled)，方案为 GUID 分区图

4、重新安装系统

### latex try


$t=\sqrt{ma}$

$c = \sqrt{a^{2}+b_{xy}^{2}+e^{x}}$

$x^2$
