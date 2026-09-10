Domain & Service Keeper (域名与服务保活看板)
一个基于 Cloudflare Workers + Cloudflare KV 搭建的轻量级、完全免费的域名与免费服务续期保活看板。

帮助你集中统一管理手头的几十个收费域名及需要定期登录/续期的免费服务（如 EU.org、Freenom、甲骨文云保活等），按剩余天数动态排序并区分紧急状态，彻底告别忘记登录/续期导致服务被收回的尴尬。

🌟 项目亮点
完全免费：基于 Cloudflare Workers 与 KV 存储，零服务器/VPS 运行成本。

Serverless 架构：前端界面与后端 API 全合一部署，无需复杂的本地构建或 Node.js 环境。

智能天数倒计时：前端自动计算剩余天数，并根据紧急程度着色（🔴 ≤15天紧急预警、🟡 16-30天提醒、🟢 >30天正常）。

自动按紧急度排序：最快需要处理的服务/域名永远自动排在最前面。

防误触顺延逻辑：点击“已保活/续期”按钮时，会在原截止日期基础上自动顺延指定的周期天数，并带有确认弹窗，绝不覆盖长期续费记录。

安全保护：带有自定义请求秘钥保护，防止他人恶搞篡改你的域名数据。

🚀 极速部署指南
只需 2 分钟 即可完成部署：

第一步：创建 Cloudflare KV 存储
登录 Cloudflare Dashboard。

在左侧菜单找到 Storage & Databases -> KV。

点击 创建命名空间 (Create Namespace)，名称填写 DOMAIN_KV 并保存。

第二步：创建并部署 Worker
在左侧菜单点击 Workers 和 Pages (Workers & Pages) -> 创建应用程序 (Create Application) -> 创建 Worker。

输入应用名称（如 domain-keeper），点击 部署 (Deploy)。

进入编辑界面，点击 编辑代码 (Edit code)。

将本仓库中的 worker.js 代码完整复制粘贴进去，覆盖原有的示例代码。

点击右上角 Save and Deploy (保存并部署)。

第三步：绑定 KV 数据库
返回该 Worker 的管理后台，切换到 设置 (Settings) 标签页 -> 点击 Variables (变量)。

向下滚动到 KV Namespace Bindings (KV 命名空间绑定)，点击 Add binding (添加绑定)。

参数设置：

Variable name (变量名称)：DOMAIN_KV（严格大写）

KV Namespace (KV 命名空间)：选择第一步创建的 DOMAIN_KV

点击 Save and deploy (保存并部署) 即可！

🔐 常用配置与说明
管理密码设置
默认密码：默认授权秘钥为 admin123。

如何修改默认密码：
在 Cloudflare Worker 的 Settings -> Variables -> 环境变量 (Environment Variables) 中添加变量 AUTH_SECRET，值为你的自定义密码。

前端使用：打开看板页面后，点击右上角的 设置秘钥，输入你的密码即可进行添加、修改、删除及续期操作。

🛠️ 技术栈
后端/存储：Cloudflare Workers, Cloudflare KV

前端 UI：HTML5, TailwindCSS (CDN), Alpine.js, Font Awesome Icons

📄 开源协议
MIT License
