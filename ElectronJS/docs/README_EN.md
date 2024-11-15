> [!TIP]
> [中文](README.md) | **English**
>

## Use Makefile in Unix-like system 
    
[Makefile README](MAKEFILE_README_EN.md)

# Environment Compilation Instruction

EasySpider is divided into three parts:

1. Main program: Located in the ElectronJS folder.
2. Browser extension: Located in the Extension folder, i.e., the `EasySpider_en.crx` file in this folder.
3. Execution stage program: Located in the ExecuteStage folder.

This section covers the compilation instructions for the `main program`.


## Suggested Compilation Order

1. Compile the browser extension, otherwise an error will be prompted when the main program is executed that `EasySpider_en.crx` cannot be found.
2. Compile the main program, at this time the main program can run normally, but can not execute the task, can only design the task.
3. Compile the execution stage program, otherwise the task cannot be executed, can only design the task.

## Note
> [!Important]
> Remember to update the `EasySpider.crx` and `easyspider_executestage` files whenever the EasySpider extension and execution program are updated.

## Environment Setup

Taking the example of Windows x64 version.

### Browser and Driver

If you're unable to handle the tasks in this section, you can download a ready-to-use EasySpider. Simply copy the `EasySpider\resources\app\chrome_win64` folder from the downloaded files and paste it into the ElectronJS folder.

If you already have Chrome installed on your local machine, you can directly execute python3 update_chrome.py to perform the operations mentioned in the following section. Make sure to set the Chrome major version in the configuration file to match the version of Chrome installed on your machine.

Download a Chrome from the Internet: https://www.google.com/chrome/, and then put them into this folder, with name format of the following:

```
chrome_win32/ # for windows x32
chrome_win64/ # for windows x64
chrome_linux64/ # for linux x64
chrome_mac64/ # for mac x64
```

Then, download the corresponding chromedriver from the Internet on this page: https://chromedriver.chromium.org/downloads, note the **chromedriver version must match your chrome version!!!** And put them into corresponding chrome folder, with name format of the following:

```
chromedriver_win32.exe # for windows x32
chromedriver_win64.exe # for windows x64
chromedriver_linux64 # for linux x64
chromedriver_mac64 # for mac x64
```

For example, if you want to build this software on Windows x64 platform, then you should first download a Chrome for Windows x64, then copy the whole `chrome` folder to this `ElectronJS` folder and rename the folder to `chrome_win64`, assume the Chrome version you downloaded is 110; then, download a `chromedriver.exe` with version 110 for Windows x64, and put it into the `chrome_win64` folder, then rename it to `chromedriver_win64.exe`.

Finally, copy the `stealth.min.js` and `execute.bat` (for Windows x64) file in this folder to these `chrome` folders.

### NodeJS Environment


1. On Windows, you need to download `VS Build Tools 2017` (https://aka.ms/vs/15/release/vs_buildtools.exe, select and install the `Visual C++ Build Tools` component) first for the module `node-gyp` to install `node-windows-manager` (No need for other OS). Meanwhile, `Python3` needs to be installed and the environment variables need to be configured.
2. Install `NodeJS`: [https://nodejs.org/en/download/](https://nodejs.org/en/download/).
3. Run the following commands to install NodeJS packages:

```
npm install
```

## Run Instruction

Run the software in developing mode:

```sh
npm run start_direct
```

But so far can only design the task, can not execute the task, want to execute the task also need to complete the 'ExecuteStage' folder of the execution of the task program compilation instructions can be executed.

## Package Instruction

Before packaging and releasing, make sure that the task execution program `easyspider_executestage(.exe)` is placed inside the `chrome(_win64)` folder and that the browser extension `EasySpider_en.crx` is the latest version. 

After finishing developing, package software by the following command (`Git` is required):

```
npm run package
```

### For windows x64

Execute the following two CMD commands sequentially to package and publish the program. There is no need to execute the previous npm command. The process is similar for other systems.

```
package_win64.cmd
clean_and_release_win64.cmd
```

## Troubleshooting

The following commands are generally not required, but may be used during packaging:

```sh
npm install @electron-forge/cli -g
npx electron-forge import
```

If the task is stuck at the `npm install electron-squirrel-startup` step, please refer to the following tutorial on changing the source: [https://blog.csdn.net/qq_38463737/article/details/140277803](https://blog.csdn.net/qq_38463737/article/details/140277803).

If you encounter `node-gyp` related errors when running `npm run package` on Windows, you can install `electron-rebuild` and recompile the relevant modules:

```sh
npm install --save-dev electron-rebuild
npx electron-rebuild
```

Then run `npm run package` again.

