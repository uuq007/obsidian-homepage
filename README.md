# obsidian-homepage
用datacorejsx写的obsidian个人主页

# 使用教程
https://kcnmij2wvjhx.feishu.cn/wiki/QEVzwct7HiUI0gkT1wacL29qnUf

1. 快速开始
1.1 前置条件
1. 必须安装datacore插件（建议升级至最新版datacore）。其他插件无强制需求
2. 将PersonalHomepageCode.md和PersonalHomepageViewer.md放进你的obsidian仓库任意位置

- 注意：PersonalHomepageCode.md和PersonalHomepageViewer.md这两个文件放进obsidian后，不要用obsidian打开或者修改（PersonalHomepageCode.md代码很多，如果用obsidian打开它会卡住几秒钟）。每次更新版本替换掉这两个文件即可。
- 建议：在obsidian的设置菜单中，进入文件与链接→高级→忽略文件→管理，将这两个文件设置成忽略文件（支持对整个文件夹忽略，或者单个文件忽略）。设置忽略文件后，obsidian不再对忽略文件进行预读取、解析文件内容，优化性能。
- 建议搭配的插件：
1. templater：链接到templater的create new note from template命令，可以实现点击卡片或图标应用模板创建新文件
2. quickAdd：可以将多个操作注册到一个obsidian命令中，可以实现点击卡片或图标一键执行复杂指令

1.2 嵌入主页
新建主页文件：在你指定的任意位置新建笔记，笔记内容为 ![[PersonalHomepageViewer]]即可

```
![[PersonalHomepageViewer]]
```

更多详见 https://kcnmij2wvjhx.feishu.cn/wiki/QEVzwct7HiUI0gkT1wacL29qnUf
