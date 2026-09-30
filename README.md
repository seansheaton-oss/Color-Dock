# Color Dock · support and ad configuration

运营者：john · 联系邮箱：seansheaton@gmail.com

- 隐私政策：https://seansheaton-oss.github.io/privacy.html
- 支持页面：https://seansheaton-oss.github.io/support.html
- 广告开关：https://seansheaton-oss.github.io/admob-ios.json
- AdMob 验证：https://seansheaton-oss.github.io/app-ads.txt

## 切换广告

编辑 `admob-ios.json` 的 `mode`，提交到 main：

| 值 | 效果 |
| --- | --- |
| `disabled` | 停止新的广告请求 |
| `test` | Google 官方测试广告位（当前默认） |
| `production` | 使用应用内配置的正式激励和插屏广告位 |

游戏在启动、回到前台及每 5 分钟获取一次。GitHub Pages 部署和缓存可能额外延迟。播放中的广告结束后应用新模式。所有用户使用同一配置，包括审核人员。

`expires_at` 是 Unix 秒，必须在未来 31 天以内。发布时请更新为当前时间加 30 天；过期、网络失败、无效内容或 Bundle ID 不匹配会关闭新广告。可在浏览器开发工具计算 `Math.floor(Date.now()/1000)+30*86400`，或在游戏工程运行：

```sh
python3 tools/make_ad_policy.py --bundle-id com.colordock.game --mode test --days 30 --output release/github/admob-ios.json
```

当前 `com.colordock.game` 仅匹配未签名开发工程。确定正式 Bundle ID 后，必须同时更新应用和此文件。正式广告 ID 保存在 iOS 工程中；本文件只控制模式，不能远程更改应用 ID、广告位、代码或同意机制。切换为关闭不代表已初始化的第三方 SDK 完全停止所有数据处理。

## 发布

GitHub Settings → Pages → Deploy from a branch → main / (root)。只发布此目录内的公开页面与配置，不要上传游戏源码、签名证书、密钥或 SDK。隐私政策已覆盖英文、简中、繁中、日文、韩文。
