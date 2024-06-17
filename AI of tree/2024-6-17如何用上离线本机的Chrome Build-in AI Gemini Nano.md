---
title: 2024-6-17如何用上离线本机的Chrome Build-in AI Gemini Nano
tags: 
grammar_cjkRuby: true
---


如何用上离线本机的Chrome Build-in AI
　　最近谷歌在新版的 Chrome 浏览器里面开放了Build-in AI的权限，用户由此可以下载Gemini Nano这个LLM到本机，不联网直接使用。用法如下：
　　1）点击Chrome浏览器的 ⋮ → 设置 → 关于Chrome，查看版本号，保证在127以上。如果
低于127，下载最新的Chrome Dev（ https://google.com/chrome/dev/ ）。
　　2）地址栏键入chrome://flags/#optimization-guide-on-device-model， 选择 Enabled
BypassPerfRequirement 。
　　3）地址栏键入chrome://flags/#prompt-api-for-gemini-nano，选择Enabled
　　4）等待模型下载完，如果下载完，chrome://components/ 会出现 Optimization Guide On
Device Model 。有人很快就看到这个选项，我等了一天多。出现了 Optimization Guide On Device Model 选项后，点击按钮，“是否有最新更新”。
　　5）命令行程序中输入git clone https://github.com/fifteen42/localhostai
　　6）输入cd localhostai
　　7）输入npm install（注，在此之前机器要装了 Node.js。Node.js 的安装可以自己搜索）
　　8）输入npm run dev，这样很快就生成了 http://localhost:3000
　　9）用新浏览器打开这个地址，就可以说用这个离线 AI 了。