# 白描桌面版

白描桌面版是基于 [Tauri](https://github.com/tauri-apps/tauri) 实现的跨平台 OCR 软件，目前支持 Windows 7+ 和 macOS 10.13+，与 [白描 App](https://baimiao.uzero.cn/) 手机端、网页端会员账号通用。

## Features

- 快捷键截屏文字识别
- 自动复制结果到粘贴板
- 对识别结果智能段落排版
- 图片、PDF 文字识别
- LaTex 公式识别
- 图片转电子表格
- 二维码 / 条形码识别
- 浅色 / 深色模式
- 多语言支持（简/繁/英/日）
- 支持开机自启动
- 离线文字识别（macOS）
- 本地服务器模式提供 API 访问（macOS）

## 已知问题

- [ ] Win7 下截图无法正常使用
- [ ] Win7 下托盘菜单可能出乱码 [tauri-apps/tauri#4966](https://github.com/tauri-apps/tauri/issues/4966)


## Links

接口文档：[API.md](API.md)

版本发布：[RELEASES.md](RELEASES.md)

下载地址：[macOS](https://cdn.desktop.baimiaoapp.com/updater/download/latest/baimiao_universal.dmg) | [Windows](https://cdn.desktop.baimiaoapp.com/updater/download/latest/baimiao.msi)


## 截图
<div align="center" >
  <img src="./screenshots/main.png" width="99%" />
  <img src="./screenshots/quick.png" width="99%" />
  <img src="./screenshots/settings-1.png" width="99%" />
  <img src="./screenshots/settings-2.png" width="99%" />
  <img src="./screenshots/settings-3.png" width="99%" />
</div>
