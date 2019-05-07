Firstly：
安装node.js   设置node.js国内镜像速度更快
搭建electron打包环境
使用node.js的npm命令安装electron和electron-packager
安装electron : npm install -g electron
安装electron-packager: npm install -g electron-packager

Secondly:
创建一个项目文件夹 
在文件夹下有三个文件


1.项目的入口 index.html （一般为登录页，index里面的css和js文件）


引用的css和js文件要和index同级

2.main.js 文件内容

'use strict';
const electron = require('electron');
const app = electron.app; // 控制App生命周期的模块
const BrowserWindow = electron.BrowserWindow; // 创建原生窗口的模块
// 保持对窗口对象的全局引用。如果不这么做的话，JavaScript垃圾回收的时候窗口会自动关闭
var mainWindow = null;
// 当所有的窗口关闭的时候退出应用
app.on('window-all-closed', function() {
// 在 OS X 系统里，除非用户按下Cmd + Q，否则应用和它们的menu bar会保持运行
if (process.platform != 'darwin') {
app.quit();
}
});
// 当应用初始化结束后调用这个方法，并渲染浏览器窗口
app.on('ready', function() {
// 创建一个窗口
mainWindow = new BrowserWindow({width:1500, height:1000, closable: true});
// 加载index.js
mainWindow.loadURL('file://' + __dirname + '/index.html');
// 打开 DevTools
//mainWindow.webContents.openDevTools();
// 窗口关闭时触发
mainWindow.on('closed', function() {
// 如果你的应用允许多个屏幕，那么可以把它存在Array里。
// 因此删除的时候可以在这里删掉相应的元素
mainWindow = null;
});
});
注: 其中只需要修改 mainWindow.loadURL参数你的页面名称

3.package.json的内容

{
"name": "targetOffline",
"version": "1.0.1",
"main": "main.js",
"dependencies": {
"electron": "^1.6.11"
},
"devDependencies": {
"electron-packager": "^8.7.2"
},
"scripts": {
"packager":"electron-packager . targetOffline --platform=win32 --overwrite "
}
}
注: 改改名称name和版本号就行,还有scripts下的应用名称(targetOffline),改为你想要的应用名称,和name对应,其实这个文件是自动生成的,可以使用npm init命令来初始化项目(过程中就会需要填入一下数据如name来生成一个package.json文件)


Third:
以上三个文件都准备好后 

切换到打包的文件夹下使用命令     electron .       来预览打包后的页面，
需注意的是:打包的文件夹下需要有通过npm下载的electron 和electronic-packager 组件
如果没有去下载后保存的路径copy过来，windows根目录下



,如果没问题,则开始打包正式的
打包命令如下:
electron-packager . targetOffline --platform=win32 --overwrite
其实就是package.json里scripts下的命令
targetOffline 是你的应用名称,
--platform 是打包成对应的系统(win32打包后的应用可以在32和64位系统里使用)


打包后的目录




fouth:
1.安装inno setup,是为了用来执行.iss文件,这种格式的文件是编写生成安装包的代码文件
文件内容:
; 脚本由 Inno Setup 脚本向导 生成！
; 有关创建 Inno Setup 脚本文件的详细资料请查阅帮助文档！
#define MyAppName "targetOfflineApp"
#define MyAppVersion "1.0"
#define MyAppPublisher "中科恒运"
#define MyAppURL "www.zkhy.com"
#define MyAppExeName "targetOfflineApp.exe"
[Setup]
; 注: AppId的值为单独标识该应用程序。
; 不要为其他安装程序使用相同的AppId值。
; (生成新的GUID，点击 工具|在IDE中生成GUID。)
AppId={{29762B12-065B-4C90-A76C-C0E6EDE4C6F0}
AppName={#MyAppName}
AppVersion={#MyAppVersion}
;AppVerName={#MyAppName} {#MyAppVersion}
AppPublisher={#MyAppPublisher}
AppPublisherURL={#MyAppURL}
AppSupportURL={#MyAppURL}
AppUpdatesURL={#MyAppURL}
DefaultDirName={pf}\{#MyAppName}
DefaultGroupName={#MyAppName}
OutputDir=D:\xm\patchLDH\setup_offline
OutputBaseFilename=offline_setup64
SetupIconFile=D:\xm\patchLDH\net.ico
Compression=lzma
;Compression=none
SolidCompression=yes
;DiskSpanning=true
;DiskSliceSize=2100000000
 
[Languages]
Name: "chinesesimp"; MessagesFile: "compiler:Default.isl"
 
[Tasks]
Name: "desktopicon"; Description: "{cm:CreateDesktopIcon}"; GroupDescription: "{cm:AdditionalIcons}"
 
[Files]
Source: "D:\xm\patchLDH\app\*"; DestDir: "{app}"; Flags: ignoreversion recursesubdirs createallsubdirs
; 注意: 不要在任何共享系统文件上使用“Flags: ignoreversion”
 
[Icons]
Name: "{group}\{#MyAppName}"; Filename: "{app}\{#MyAppExeName}"; WorkingDir: "{app}"
Name: "{group}\{cm:UninstallProgram,{#MyAppName}}"; Filename: "{uninstallexe}"; WorkingDir: "{app}"
Name: "{userdesktop}\{#MyAppName}"; Filename: "{app}\{#MyAppExeName}"; Tasks: desktopicon; WorkingDir: "{app}"
 
[Run]
Filename: "{app}\mybat\startMySQL.bat"; Flags: runhidden
Filename: "{app}\mybat\startTomcat.bat"; Flags: runhidden
Filename: "{app}\{#MyAppExeName}"; Description: "{cm:LaunchProgram,{#StringChange(MyAppName, '&', '&&')}}"; Flags: nowait postinstall skipifsilent
 
[UninstallRun]
Filename: "{app}\mybat\deleteTomcatService.bat"; Flags: RunHidden;
Filename: "{app}\mybat\deleteMySqlTestService.bat"; Flags: RunHidden;
 
注:只需要修改MyAppName ,MyAppExeName ,AppId,SetupIconFile,Source(后面三个为改路径)
 
2.代码编辑好后,在.iss文件同级目录下新建一个文件夹app,并把之前electron-packager打包好的文件目录全部复制到此app下来,如图所示

把打包好的文件夹下的所有东西copy到app 文件夹，运行iss 就OK了
