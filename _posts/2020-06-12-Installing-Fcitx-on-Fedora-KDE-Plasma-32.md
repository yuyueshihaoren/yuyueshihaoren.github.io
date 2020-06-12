English:

This tutorial focuses on installing fcitx input method on Fedora 32 KDE Plasma on Wayland

First, update the repository. `sudo dnf update`.

Then, install fcitx and your input method (for example, libpinyin) and the configure tool of fcitx (the KDE version)
```shell
sudo dnf install fcitx fcitx-libpinyin fcitx-qt4 kcm-fcitx
```

After installing all the packages, run `fcitx-configtool` either through terminal or start menu and add your input method. Note that if your system language isn't the same as the input method that you are going to install, you'll need to tick off the "Only Show Current Language" checkbox. Hit Apply or OK and quit.

Run this command in your terminal
```shell
imsettings-switch -s fcitx
```

You might get warnings here. Just ignore it. Log out and log back in or reboot. You should be ready to go.


简体中文：

这篇教程简短地讨论一下在Fedora 32 KDE Plasma Wayland上安装fcitx.

首先，更新一下系统。`sudo dnf update`

然后，安装fcitx输入法框架和你想要装的输入法（这里以libpinyin为例），以及KDE上的配置工具
```shell
sudo dnf install fcitx fcitx-libpinyin fcitx-qt4 kcm-fcitx
```

安装好以后，运行fcitx，再运行fcitx-configtool。在配置选项里加入输入法。如果系统语言为英文，记得勾选掉下面的“Only Show Current Language”选项。然后点击应用。

运行一下命令来切换系统默认输入法至fcitx
```shell
imsettings-switch -s fcitx
```

此处会有报错，请忽略，然后重启电脑。安装完成。