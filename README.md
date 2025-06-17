# Linux-Walkthrough
This repository keeps track of the path of exploring linux systems, including necessary reminders and step instructions. Resources used in this repository would be shared publicly, honoring the creators and contributers to all the splendid tools.

# Arch Linux
Best Linux distribute ever!!
![Arch Linux chan](/Resources/Image/ArchLinux.png)
(Credit: [@RavioliMavioli](https://krita-artists.org/t/archlinux-chan/49206))(After AI processed)
## Necessary Setup
### Arch User Repository (AUR) helper
---
To install packages on a Arch Linux machine, one good option is to use `pacman`[package manager](https://wiki.archlinux.org/title/Pacman) that's been integrated to the system on installation.
While [Arch User Repository(AUR)](https://wiki.archlinux.org/title/Arch_User_Repository) also supports thousands and millions of useful packages, we should employ a helper to install from AUR.
In this guide, we are using `yay` as the default AUR helper.
To install `yay`, see the [github page of yay](https://github.com/Jguer/yay).

### Language display
---
Upon first installation of Arch Linux system, the system is generally in full English and does not support any other languages. Other languages (like Chinese) is not recognizable and therefore displayed as blocks. This is because:
1. Specific language support not enabled due to **locale** settings.
2. Missing corresponding **fonts**.

We should solve this issue step by step.

#### Modifying locale settings
First of all, run the following command to see your current set locale and its related environmental settings.
```
locale
```
In arch linux, the locale.gen file in `/etc/locale.gen` controls what languages should be enabled. Locate to the file and uncomment the languages you'd like to enable. For example:
```
#iu_CA UTF-8  
#ja_JP.EUC-JP EUC-JP  
ja_JP.UTF-8 UTF-8  //Uncomment the desired language(s) here.
#ka_GE.UTF-8 UTF-8  
#ka_GE GEORGIAN-PS  
```
(See more information [here](https://wiki.archlinux.org/title/Locale).)

CAUTION: DO NOT mix use the encoding methods. If you've chosen UTF-8, then keep it consistent for the remaining languages.

Then, save and close the file, and run:
```
locale-gen
```
You can check the archived (ready to use) language packs by running:
```
localedef --list-archive
```
**Please move to the installation of fonts if you DO NOT want to change the display language of the system.**

To change the system interface, after running `locale-gen`, go to `/etc/locale.conf`. Set the variable LANG to your desired language code. For example:
```
LANG=ja_JP.UTF-8 UTF-8
```
What's more, without changing the LANG variable, you could also modify the display language with:
```
LANG=en_US.UTF-8
LANGUAGE=ja_JP
```

See [this link](https://wiki.archlinux.org/title/Locale#Variables) for more information.

#### Installing missing fonts
After finishing the locale settings, download the missing fonts on Arch wiki by searching "Localization/<DESIRED LANGUAGE>". For example, the  [Arch wiki page](https://wiki.archlinux.org/title/Localization/Chinese) for Chinese localization.

The installation of fonts on linux should be very straight forward.

After completing the steps, reboot your system, and you should see the languages displayed normally.

### Input method
---
The general steps for employing a multi-languages input method on Arch Linux are as follows.
1. Install a input method package.
2. Install correspoding language add-ons.
3. (Specially on gnome Arch Linux) Solve the problem that there isn't pop up window while typing.
4. Configure the input method.
5. Set the environment variables to tell the programs on your machine to use this input method.

The guide of this section would be based on gnome Arch Linux system, using a fcitx5 input method, and with Chinese and Japanese add-ons. All contents below is based on [Arch wiki of Fcitx5](https://wiki.archlinux.org/title/Fcitx5).

#### Install the input method package
In this guide, we will install the [fcitx5 package](https://archlinux.org/packages/?name=fcitx5) as example.
If you have the AUR helper `yay` installed, run
```
yay -S fcitx5
```
to install the fcitx5 package.
For other methods, make use of the internet.

CAUTION: You SHOULDN'T rely fully on the code listed above. Because the package would be updated and its name might change. Follow the link to see the real-time and latest package name to install is the best choice. The same caution is also applicable to all the installation-related code in this document.

#### Install corresponding language add-ons
For Chinese language add-ons, the package [fcitx5-chinese-addons](https://archlinux.org/packages/?name=fcitx5-chinese-addons) is recommended. Run
```
yay -S fcitx5-chinese-addons
```
to install.

For Japanese language add-ons, the package [fcitx5-mozc](https://archlinux.org/packages/?name=fcitx5-mozc) is recommended. Run
```
yay -S fcitx5-mozc
```
to install.

For more language add-ons for Chinese and Japanese, see the [Arch wiki page](https://wiki.archlinuxcn.org/wiki/Fcitx5) or search the web.

#### (Gnome Arch Linux ONLY) Install gnome extension to activate pop-up window
Based on the [fcitx5 Arch wiki](https://wiki.archlinux.org/title/Fcitx5#GNOME), if you have installed your system with gnome profile, the pop up window might not appear.

Install [Input Method Panel Extension](https://extensions.gnome.org/extension/261/kimpanel/) and ACTIVATE it on the `extension` app would later appear after installing the extension.

#### Configure the input method using GUI
You could also use command line to configure the input method. But you would find it more convenient and faster to use the GUI application [fcitx5-configtool](https://archlinux.org/packages/?name=fcitx5-configtool). Run
```
yay -S fcitx5-configtool
```
to install the application. The application would be added to your app library. You could also launch the app by runnning:
```
fcitx5-configtool
```

Then, find the language add-ons you have installed just before, and configure it properly.
Mind that the Chinese add-ons usually appear on the **bottom** of the application, and they WON'T appear if you search "Chinese". The Japanese add-ons has a simple name of "mozc". Configuring the wrong language input method won't make an effect.

#### Set the environment variables to enable input method thourgh out the machine
Navigate to `/etc/environment`, and add these two lines to the file:
```
QT_IM_MODULE=fcitx5
XMODIFIERS=@im=fcitx5
```
CAUTION: If your installation environment is not the same with the guide (such as input method is not fcitx5, or your machine is not gnome running Arch Linux), you should search the web for the environment variable configuration. You could navigate to this [Arch wiki](https://wiki.archlinuxcn.org/wiki/Fcitx5#%E9%85%8D%E7%BD%AE) for more information.

Finally, reboot your system to let the input method take effect.
