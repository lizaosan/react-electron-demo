# React + Electron + Electron packager

## 快速上手

1. `npx create-react-app react-electron-demo`
2. `cd react-electron-demo`
3. `npm install electron`
4. `npm install electron-packager --save-dev`
5. 編輯根目錄 package.json `"homepage": "./",`
6. `npm run build`
7. `cd build`
8. build 創建 main.js
9. build 創建 package.json
10. `npm run package`

```jsx
/*main.js*/

const electron = require("electron");
const { app } = electron;
const { BrowserWindow } = electron;

let win;

function createWindow() {
	win = new BrowserWindow({ width: 1920, height: 1080 });

	win.loadURL(`file://${__dirname}/index.html`);

	//win.webContents.openDevTools();

	win.on("closed", () => {
		win = null;
	});
}

app.on("ready", createWindow);
/* var mainWindow = new BrowserWindow({
  webPreferences: {
    nodeIntegration: false
  }
}); */
app.on("window-all-closed", () => {
	if (process.platform !== "darwin") {
		app.quit();
	}
});

app.on("activate", () => {
	if (win === null) {
		createWindow();
	}
});
```

```jsx
/*package.json*/
{
	"name": "react-electron-demo",
	"version": "0.1.0",
	"main": "main.js",
	"scripts": {
		"electron": "electron .",
		"package": "electron-packager . react-electron-demo --platform=win32 --arch=x64 --electron-version=12.0.5 --overwrite --icon=./favicon.ico"
	}
}

```

## 資源

[Electron | Build cross-platform desktop apps with JavaScript, HTML, and CSS.](https://www.electronjs.org/)

[Quick Start Guide | Electron](https://www.electronjs.org/docs/tutorial/quick-start)

[electronPackager | electron-packager](https://electron.github.io/electron-packager/master/modules/electronpackager.html)

[在 React 中使用 Electron](https://segmentfault.com/a/1190000039729774)

[electron 原来这么简单----打包你的 react、VUE 桌面应用程序](https://segmentfault.com/a/1190000014030465?utm_source=sf-similar-article)
