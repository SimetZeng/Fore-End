# 概述
目前主流的包管理工具有npm、yarn、pnpm，下文是个人对npm和yarn的理解。

## npm
npm使用一个  `package.json` 的文件，用户可通过 `npm install -g(--save/--save-dev)` 命令把项目里所有依赖项保存到这个文件里

## yarn
- 每个yarn安装都会生成一个yarn.lock文件, 除去常规信息之外，还包含要安装的内容的校验和，以确保使用的库的版本相同。
- yarn无需互联网连接就能安装本地缓存的依赖项，并提供了离线模式。[点击下载安装](https://yarnpkg.com/zh-Hans/docs/install)。


### 参考文献
http://geek.csdn.net/news/detail/197339
