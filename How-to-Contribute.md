# Contributing to Code
There are many great ways to contribute to the Code project: logging bugs, submitting pull requests, and creating suggestions.

## Build and Run From Source

If you want to understand how Code works or want to debug an issue, you'll want to get the source, build it, and run the tool locally.

### Installing Prerequisites

[Download the latest version](https://code.visualstudio.com/Download) of Visual Studio Code (you will use VS Code to edit Code!)

Code includes node module dependencies that require native compilation. To ensure the compilation is picking up the right version of header files from the Electron Shell, we have our own script to run the installation via npm.

**Tip!** In case you fail to build the native modules you can copy the node_modules folder of the VS Code installation into the `vscode` workspace node_modules folder. You will still need to run our unpm install to get all the development dependencies.

For native compilation, you will need python (version `v2.7` recommended, `v3.x.x` is __*not*__ supported) as well as a C/C++ compiler tool chain.

**Windows:**
* In addition to Python v2.7, make sure you have a PYTHON environment variable set to `drive:\path\to\python.exe`, not to a folder
* Visual Studio 2013 for Windows Desktop or [Visual Studio 2015](https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx) , make sure to select the option to install all C++ tools and the Windows SDK

**OS X** Command line developer tools
* Python should be installed already
* [XCode](https://developer.apple.com/xcode/downloads/) and the Command Line Tools (XCode -> Preferences -> Downloads), which will install `gcc` and the related toolchain containing `make`

**Linux:**
* Python v2.7
* `make`
* A proper C/C++ compiler toolchain, for example [GCC](https://gcc.gnu.org)

After you have these tools installed, run the following commands to check out Code and install dependencies:

OS X

	git clone https://github.com/microsoft/vscode
	cd vscode && npm install -g mocha gulp
	./scripts/npm.sh install

Windows

	git clone https://github.com/microsoft/vscode
	cd vscode
	npm install -g mocha gulp
	scripts\npm install

Linux

	git clone https://github.com/microsoft/vscode
	cd vscode && npm install -g mocha gulp
	./scripts/npm.sh install --arch=x64
	# for 32bit Linux
	#./scripts/npm.sh install --arch=ia32

## Development Workflow

### Incremental Build
Open VS Code on the folder where you have cloned the `vscode` repository and press `CMD+SHIFT+B` (`CTRL+SHIFT+B` on Windows, Linux) to start the TypeScript builder. It will do an initial full build and then watch for file changes, compiling those changes *incrementally*. To view the build output open the Output stream by pressing `CMD+SHIFT+U`.

### Errors and Warnigns
Errors and warnings are indicated in the status bar at the bottom left. You can view the error list using `View | Errors and Warnings` or pressing `CMD+P` and then `!`. Please note, if you start the TypeScript builder from a terminal using `gulp watch`, errors and warnings will only show in the console and not in Code.

**Tip!** You do not need to stop and restart the development version after each change, you can just execute `Reload Window` from the command palette.

### Validate your changes
To test the changes you launch a development version of VS Code on the workspace `vscode`, which you are currently editing.

OS X and Linux

	./scripts/code.sh

Windows

	.\scripts\code.bat

You can identify the development version of Code by the Electron icon in the Dock or Taskbar.

**Tip!** If you receive an error stating that the app is not a valid Electron app, it probably means you didn't run `gulp watch` first.

### Debugging
Code has a multi-process architecture and your code is executed in different processes.

The **render** process runs the UI code inside the Shell window. To debug code running in the **renderer** you can either use VS Code or the Chrome Developer Tools.

#### Using VSCode
* Install the [Debugger for Chrome](https://marketplace.visualstudio.com/items/msjsdiag.debugger-for-chrome) extension. This extension will let you attach to and debug client side code running in Chrome.
* Launch the development version of Code with the following command line option:

OSX and Linux
``` bash
./scripts/code.sh --remote-debugging-port=9222
```
Windows
``` bash
scripts\code --remote-debugging-port=9222
```

* Choose the `Attach to VSCode` launch configuration from the launch dropdown in the Debug viewlet and press `F5`.


#### Using the Chrome Developers Tools

* Run the `Developer: Toggle Developer Tools` command from the Command Palette in your development instance of Code to launch the Chrome tools.

The **extension host** process runs code implemented by a plugin. To debug extensions (including those packaged with Code) which run in the extension host process, you can use VS Code itself. Switch to the Debug viewlet, choose the `Attach to Extension Host` configuration, and press `F5`.

### Unit Testing
Press `CMD+SHIFT+T` (`CTRL+SHIFT+T` on Windows) to start the unit tests or run the tests directly from a terminal by running `./test/run.sh` from the `vscode` folder (`test\run` on Windows). The [test README](/test/README.md) has complete details on how to run and debug tests, as well as how to produce coverage reports.

## Pull Requests
Before we can accept a pull request from you, you'll need to sign a [[Contributor License Agreement (CLA)|Contributor-License-Agreement]]. It is an automated process and you only need to do it once. The project [README.md](https://github.com/Microsoft/vscode/blob/master/README.md) details how to clone, build, run, debug and test Code. Be sure to follow our [[Coding Guidelines|Coding-Guidelines]].

## Suggestions
We're also interested in your feedback in future of Code. You can submit a suggestion or feature request through the issue tracker. To make this process more effective, we're asking that these include more information to help define them more clearly. 

## Discussion Etiquette

In order to keep the conversation clear and transparent, please limit discussion to English and keep things on topic with the issue. Be considerate to others and try to be courteous and professional at all times.