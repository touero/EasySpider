> [!TIP]
> [中文](MAKEFILE_README.md) | **English**
>

## Environment Setup
Make sure you are in the root directory of EasySpider and have installed Node.js, npm, chrome, corresponding versions of chromedriver and python.
Ensure that Node.js, npm, Chrome, the corresponding version of Chromedriver, and Python are installed.

## Parameter Description

### Program Parameters
The default testing parameters are for Ubuntu. If using a different system, please modify them according to your actual situation.
1. `ROOT_DIR`: The root directory of the project. By default, it is the current project directory, i.e., under EasySpider.
2. `CHROME_DIR`: The directory where Chrome is installed.
3. `SYSTEM`: The system type. By default, it is `linux64`. Options: `linux64`, `mac64`.
4. `CHROMEDRIVER_DIR`: The path to Chromedriver, which has no default value.
5. `CHROMEDRIVER_SUFFIX`: The suffix for Chromedriver, defaulting to `linux64`. Options: `linux64`, `mac64`.

### Make Parameters
1. `dependency`: Install Ubuntu dependencies.
2. `extension`: Only compile the browser extension.
3. `chrome`: Copy the Chrome browser to the specified directory.
4. `chromedriver`: Copy Chromedriver to the specified directory.
5. `electron`: Only compile the ElectronJS main program.
6. `clean_extension`: Clean up browser extension npm dependencies.
7. `clean_electron`: Clean up ElectronJS main program dependencies.
8. `all`: Execute steps 1-5.
9. `dev`: Execute steps 6-7, then steps 2-5. Removes npm dependencies and recompiles, primarily used during development.
10. `clean`: Execute steps 6-7 to clean up browser extensions and ElectronJS main program.

## Usage
After setting up the environment on Ubuntu, run the following command:
```shell
make CHROMEDRIVER_DIR=~/Downloads/chromedriver
```
The full command is:
```shell
make CHROME_DIR=/opt/google/chrome SYSTEM=linux64 CHROMEDRIVER_PATH=~/Downloads/chromedriver CHROMEDRIVER_SUFFIX=linux64
```

To clear npm dependencies and recompile:
```shell
make clean
```

For development, use the following command:
```shell
make dev CHROMEDRIVER_DIR=~/Downloads/chromedriver
```

