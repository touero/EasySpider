> [!TIP]
> **中文** | [English](MAKEFILE_README_EN.md) 
>



## 环境构建
确保处于EasySpider根目录下，且已经安装了Node.js、npm、chrome、对应版本的chromedriver和python。   

## 参数说明

### 程序参数
测试参数默认为Ubuntu系统，若使用其他系统，请根据实际情况修改。   
1. `ROOT_DIR`：项目根目录，默认为当前项目目录，即EasySpider下
2. `CHROME_DIR`: chrome安装目录
3. `SYSTEM`: 系统类型，默认为`linux64`，可选: `linux64`, `mac64`
4. `CHROMEDRIVER_DIR`: chromedriver路径，不存在默认值
5. `CHROMEDRIVER_SUFFIX`: chromedriver后缀名，默认为`linux64`，可选：`linux64`, `mac64`

### make参数
1. `dependency`: 安装Ubuntu依赖
2. `extension`：只编译浏览器扩展
3. `chrome`：复制chrome浏览器到指定目录
4. `chromedriver`：复制chromedriver到指定目录
5. `electron`：只编译ElectronJS主程序
6. `clean_extension`：清理浏览器扩展npm依赖
7. `clean_electron`: 清除ElectronJS主程序依赖
8. `all`: 包括1-5步骤
9. `dev`: 6-7, 2-5步骤, 移除npm依赖重新, 开发多使用
10. `clean`: 6-7步骤, 清理浏览器扩展和ElectronJS主程序

## 运行
在Ubuntu下, 构建好环境后：
```shell
make CHROMEDRIVER_DIR=~/Downloads/chromedriver
```
它完整的是：
```shell
make CHROME_DIR=/opt/google/chrome SYSTEM=linux64 CHROMEDRIVER_PATH=~/Downloads/chromedriver CHROMEDRIVER_SUFFIX=linux64
```
想清除npm依赖后重新编译：
```shell
make clean
```
开发过程多用：
```shell
make dev CHROMEDRIVER_DIR=~/Downloads/chromedriver
```
