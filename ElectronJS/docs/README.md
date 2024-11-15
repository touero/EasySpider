> [!TIP]
> **中文** | [English](README_EN.md) 
>

## 视频教程

[从源代码编译程序并设计运行和调试任务指南（基于Ubuntu24.04）](https://www.bilibili.com/video/BV1VE421P7yj/)

## 在类Unix系统上使用Makefile
    
[Makefile README](MAKEFILE_README.md)

# 环境编译说明

EasySpider分三部分：

1. 主程序：在`ElectronJS`文件夹下。
2. 浏览器扩展：在`Extension`文件夹下，为浏览器的“操作台”的代码，打包后的扩展在此目录下的`EasySpider_zh.crx`文件。
3. 执行阶段程序：在`ExecuteStage`文件夹下。

此部分为`主程序`的编译说明。


## 建议编译顺序

1. 编译浏览器扩展，否则在主程序执行时会提示找不到`EasySpider_zh.crx`的错误。
2. 编译主程序，此时主程序可以正常运行，但无法执行任务，只能设计任务。
3. 编译执行阶段程序，否则无法执行任务，只能设计任务。


## 注意事项
> [!Important]
> 请记住，每当EasySpider扩展程序和执行程序更新时，都要更新`EasySpider.crx`和`easyspider_executestage`文件。  

## 环境构建

以下以Windows x64版本为例。

### 浏览器和驱动

实在搞不定本节的情况下，下载一个直接能用的EasySpider，并把文件夹内的`EasySpider\resources\app\chrome_win64`文件夹拷贝到此`ElectronJS`文件夹下即可。

在自己的机器环境已经安装了Chrome的情况下，直接执行`python3 update_chrome.py`也可以完成本节下面写的一系列的操作，注意设置文件中的Chrome大版本号为本机Chrome的版本号。

下载一个Chrome：[https://www.google.com/chrome/](https://www.google.com/chrome/)，然后找到Chrome安装后的文件夹，如`C:\Program Files\Google\Chrome\Application`，把这个文件夹拷贝到此`ElectronJS`文件夹内，并按照以下格式更名：

```
chrome_win32/ # for windows x32
chrome_win64/ # for windows x64
chrome_linux64/ # for linux x64
chrome_mac64/ # for mac x64
```

然后，从下面的页面下载和**自己安装的Chrome版本一致**的Chromedriver：[https://googlechromelabs.github.io/chrome-for-testing/](https://googlechromelabs.github.io/chrome-for-testing/)，把chromedriver放入刚刚的`chrome`文件夹内，并更名为下面的格式：

```
chromedriver_win32.exe # for windows x32
chromedriver_win64.exe # for windows x64
chromedriver_linux64 # for linux x64
chromedriver_mac64 # for mac x64
```

例如，如果您想在Windows x64平台上构建此软件，那么您首先需要下载适用于Windows x64的Chrome浏览器，并将整个`chrome`文件夹复制到`ElectronJS`文件夹中，然后将文件夹重命名为`chrome_win64`。假设您下载的Chrome版本是110。接下来，下载一个适用于Windows x64的110版本的ChromeDriver，并将其放入`chrome_win64`文件夹中，然后将其重命名为`chromedriver_win64.exe`。

最后，把此文件夹内的`stealth.min.js`和`execute.bat`文件拷贝入`chrome`文件夹内。 


### NodeJS环境

1. Windows环境下需要先下载`VS Build Tools 2017` （[https://aka.ms/vs/15/release/vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)）并勾选安装其中的`Visual C++ Build Tools（Visual C++生成工具）`组件以便`node-gyp`模块来安装`node-windows-manager`，不然下面的命令无法执行，其他系统不需要。同时，`Python3`也需要安装在系统中并配置好环境变量。
2. 安装`NodeJS`：[https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)。
3. 运行下面的命令来安装依赖：

```
npm install
```

如果上面的命令运行速度很慢可以参考使用NodeJS和Electron包的换源说明来加速安装：[https://blog.csdn.net/qq_38463737/article/details/140277803](https://blog.csdn.net/qq_38463737/article/details/140277803)。


## 运行说明

在当前文件夹执行以下命令即可在开发模式下运行程序：

```sh
npm run start_direct
```

但到此为止只能设计任务，不能执行任务，想要执行任务还需要完成`ExecuteStage`文件夹下的执行任务程序的编译说明才可以执行。

## 打包发布说明

打包发布前，确保执行阶段程序`easyspider_executestage(.exe)`已放入`chrome(_win64)`文件夹内，且浏览器插件`EasySpider_zh.crx`已经是最新版本。

执行下面的命令即可打包（需要安装`Git`）：

```
npm run package
```


### For windows x64

依次执行下面两个cmd即可打包并发布，无需执行上面的npm命令，其他系统同理。

```
package_win64.cmd
clean_and_release_win64.cmd
```

## 可能出现的问题

以下命令一般不需要执行，但打包时可能会用到：

```sh
npm install @electron-forge/cli -g
npx electron-forge import
```

如果任务执行到`npm install electron-squirrel-startup`的步骤时卡死，请参考下面的换源教程：[https://blog.csdn.net/qq_38463737/article/details/140277803](https://blog.csdn.net/qq_38463737/article/details/140277803)。

Windows端如果在运行`npm run package`的时候提示`node-gyp`相关的错误，可以安装`electron-rebuild`并重新编译相关模块：

```sh
npm install --save-dev electron-rebuild
npx electron-rebuild
```

然后再次运行`npm run package`。

