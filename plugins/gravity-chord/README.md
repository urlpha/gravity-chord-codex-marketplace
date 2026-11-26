# GravityChord for Codex

让 Codex 直接调用引力和弦（GravityChord）生成音乐：写词、出成品歌、查进度、看作品。

## 安装

```bash
codex plugin marketplace add urlpha/gravity-chord-codex-marketplace
codex plugin add gravity-chord@gravity-chord-marketplace
```

## 授权

首次使用会提示授权，执行一次：

```bash
codex mcp login gravity-chord
```

浏览器会打开引力和弦授权页，登录后点「用当前登录账号授权」即可完成。没有账号的话先在
https://music.gravitychord.com 注册（免费）。

## 使用

直接在 Codex 里说：

```
帮我做一首适合短视频的轻松配乐，30 秒左右
```

或者更精确：

```
用 gravity-chord 生成一首 60 秒纯音乐，
caption 用英文 "warm lofi piano, soft vinyl crackle"，
instrumental 设 true，不要歌词。
```

## 说明

- 单首 90 秒曲目约 3-6 分钟出结果，600 秒约 18 分钟。工具超时已设 1800 秒。
- `caption` 必须是英文，插件内的 skill 会提醒 Codex 自动翻译。
- 额度与账号绑定，可在 https://music.gravitychord.com/api.html 查看。

MIT License
