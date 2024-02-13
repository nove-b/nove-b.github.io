---
author: ["nove-b"]
title: "Install Nuxt3"
date: "2024-02-12"
description: "Nuxt3をインストールする"
tags: ["Nuxt3"]
ShowToc: true
# draft: true
---

## 環境
- windws11
- node => v20.11.0
- npm => 10.4.0
- 
---


## install

公式の手順に従っていく。

[Installation · Get Started with Nuxt](https://nuxt.com/docs/getting-started/installation)

```
npx nuxi@latest init <project-name>
❯ Which package manager would you like to use?
● npm
○ pnpm
○ yarn
○ bun
```
上記を実行すると、エラーが発生した。

```
npm WARN cleanup Failed to remove some directories [
npm WARN cleanup   [
npm WARN cleanup     'C:\\project\\project-name\\node_modules',
npm WARN cleanup     [Error: EPERM: operation not permitted, scandir 'C:\project\project-name\node_modules\resolve\test\resolver\multirepo\packages\package-a'] {
npm WARN cleanup       errno: -4048,
npm WARN cleanup       code: 'EPERM',
npm WARN cleanup       syscall: 'scandir',
npm WARN cleanup       path: 'C:\\project\\project-name\\node_modules\\resolve\\test\\resolver\\multirepo\\packages\\package-a'
npm WARN cleanup     }
npm WARN cleanup   ],
npm WARN cleanup   [
npm WARN cleanup     'C:\\project\\project-name\\node_modules\\@vercel',
npm WARN cleanup     [Error: EPERM: operation not permitted, rmdir 'C:\project\project-name\node_modules\@vercel\nft\node_modules\@rollup\pluginutils\dist'] {
npm WARN cleanup       errno: -4048,
npm WARN cleanup       code: 'EPERM',
npm WARN cleanup       syscall: 'rmdir',
npm WARN cleanup       path: 'C:\\project\\project-name\\node_modules\\@vercel\\nft\\node_modules\\@rollup\\pluginutils\\dist'
npm WARN cleanup     }
npm WARN cleanup   ]
npm WARN cleanup ]
npm ERR! code 1
npm ERR! path C:\project\project-name\node_modules\@parcel\watcher
npm ERR! command failed
npm ERR! command C:\WINDOWS\system32\cmd.exe /d /s /c node-gyp rebuild
npm ERR! gyp info it worked if it ends with ok
npm ERR! gyp info using node-gyp@10.0.1
npm ERR! gyp info using node@20.11.0 | win32 | x64
npm ERR! gyp info find Python using Python version 3.9.6 found at "C:\Users\username\AppData\Local\Programs\Python\Python39\python.exe"
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! find VS msvs_version not set from command line or npm config
npm ERR! gyp ERR! find VS VCINSTALLDIR not set, not running in VS Command Prompt
npm ERR! gyp ERR! find VS could not use PowerShell to find Visual Studio 2017 or newer, try re-running with '--loglevel silly' for more details
npm ERR! gyp ERR! find VS not looking for VS2015 as it is only supported up to Node.js 18
npm ERR! gyp ERR! find VS not looking for VS2013 as it is only supported up to Node.js 8
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! find VS **************************************************************
npm ERR! gyp ERR! find VS You need to install the latest version of Visual Studio
npm ERR! gyp ERR! find VS including the "Desktop development with C++" workload.
npm ERR! gyp ERR! find VS For more information consult the documentation at:
npm ERR! gyp ERR! find VS https://github.com/nodejs/node-gyp#on-windows
npm ERR! gyp ERR! find VS **************************************************************
npm ERR! gyp ERR! find VS
npm ERR! gyp ERR! configure error
npm ERR! gyp ERR! stack Error: Could not find any Visual Studio installation to use
npm ERR! gyp ERR! stack at VisualStudioFinder.fail (C:\project\project-name\node_modules\node-gyp\lib\find-visualstudio.js:113:11)
npm ERR! gyp ERR! stack at VisualStudioFinder.findVisualStudio (C:\project\project-name\node_modules\node-gyp\lib\find-visualstudio.js:69:17)
npm ERR! gyp ERR! stack at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
npm ERR! gyp ERR! stack at async createBuildDir (C:\project\project-name\node_modules\node-gyp\lib\configure.js:69:26)
npm ERR! gyp ERR! stack at async run (C:\project\project-name\node_modules\node-gyp\bin\node-gyp.js:81:18)
npm ERR! gyp ERR! System Windows_NT 10.0.22621
npm ERR! gyp ERR! command "C:\\Users\\username\\AppData\\Local\\Volta\\tools\\image\\node\\20.11.0\\node.exe" "C:\\project\\project-name\\node_modules\\node-gyp\\bin\\node-gyp.js" "rebuild"
npm ERR! gyp ERR! cwd C:\project\project-name\node_modules\@parcel\watcher
npm ERR! gyp ERR! node -v v20.11.0
npm ERR! gyp ERR! node-gyp -v v10.0.1
npm ERR! gyp ERR! not ok

npm ERR! A complete log of this run can be found in: C:\Users\username\AppData\Local\npm-cache\_logs\2024-02-13T10_14_47_279Z-debug-0.log

 ERROR  Error: Command failed with exit code 1: npm install
```

エラーを見てみると`@parcel\watcher` あたりが怪しい気がする。

[@parcel/watcher](https://www.npmjs.com/package/@parcel/watcher)はどうやらファイルの監視を行う`npm`パッケージらしい。

> Set an alternative watcher that will be used as the watching service for Nuxt.
> Nuxt uses chokidar-granular by default, which will ignore top-level directories (like node_modules and .git) that are excluded from watching.
> You can set this instead to parcel to use @parcel/watcher, which may improve performance in large projects or on Windows platforms.
> You can also set this to chokidar to watch all files in your source directory.
>
> [https://nuxt.com/docs/guide/going-further/experimental-features#watcher](https://nuxt.com/docs/guide/going-further/experimental-features#watcher)

> Nuxt のウォッチングサービスとして使用される代替のウォッチャーを設定します。
> Nuxt はデフォルトで chokidar-granular を使用しており、ウォッチから除外されたトップレベルのディレクトリ（node_modules や .git など）を無視します。
> 代わりに @parcel/watcher を使用するようにこれを設定することができます。これにより、大規模なプロジェクトや Windows プラットフォームでのパフォーマンスが向上する場合があります。
> また、ソースディレクトリ内のすべてのファイルをウォッチするようにこれを chokidar に設定することもできます。

ということなのでファイルの監視に使用されるためにインストールされているっぽい。

[running into errors installing Nuxt3](https://stackoverflow.com/questions/77976536/running-into-errors-installing-nuxt3)
[Inint nuxt 3 project fails with npm package](https://stackoverflow.com/questions/77893072/inint-nuxt-3-project-fails-with-npm-package)

どうようのエラーに遭遇しているひとも結構いるっぽい。

この時点で何も気にせずにnpm installをしていたら問題なく起動していたかもしれないけど、試してないのでわからない。

大本営`Githu`でも、[Unable to install with command failed sh -c node-gyp rebuild](https://github.com/nuxt/nuxt/issues/25478)標記されているが、`Nuxt`の問題じゃないと言われている。
でその上の過程[Unable to install with command failed sh -c node-gyp rebuild](https://github.com/unjs/nitro/issues/2123)でプルリクが出されている。

で、いろいろたらいまわしにされ、[Unable to install with command failed sh -c node-gyp rebuild](https://github.com/unjs/nitro/issues/2123)で、

> If you add the following to package.json then do a clean install does it work?
> 
> "overrides": {
>    "@parcel/watcher": "2.1.0"
> },

という希望が示されていたので、実行してみた。

```$ npm i

> postinstall
> nuxt prepare

✔ Types generated in .nuxt                                                                                                                                                                                                                                19:37:24

added 732 packages, and audited 734 packages in 3m

120 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

インストールも成功し、

```
npm run dev -- -o
```

で無事にサーバーも起動した。

なんとなく気分の良くないインストール体験だった。
