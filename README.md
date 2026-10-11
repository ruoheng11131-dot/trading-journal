# 个人交易日志网站（MVP）

## 已实现
- 深色响应式界面：电脑端交易终端布局、手机端底部导航
- 总览：权益曲线、累计净盈亏、收益率、记录内最大回撤、胜率、平均盈亏、Profit Factor、当前连胜
- 今日风控：每日最大亏损、剩余风险额度
- 手动新增、编辑、删除交易
- 交易复盘：进出场、止损止盈、策略、交易时段、风险金额、纪律评分、标签、市场背景、复盘、心得
- 分析：按品种和策略汇总盈亏、纪律平均分、复盘摘要
- CSV 导出
- 本地浏览器保存
- Supabase Auth + 云端同步代码及 RLS SQL 模板

## 本地运行
1. 解压 ZIP。
2. 双击 `index.html` 可以查看本地界面。建议部署到 HTTPS 静态托管，以便稳定使用登录和云同步。
3. 先录入测试交易，检查盈亏统计是否符合预期。

## 启用云端同步（需要你自己的 Supabase 项目）
1. 在 Supabase 创建项目。
2. 打开 SQL Editor，运行 `supabase-schema.sql`。
3. 在 Authentication 设置中启用 Email 登录；创建一个个人账号，或在网站中使用邮箱注册流程。
4. 在 Project Settings → API 中复制 Project URL 和 publishable/anon key。
5. 在网站的「设置与同步」页面填入 URL、key、邮箱和密码，点击「连接 / 登录」。
6. 确认云端读写正常后，再在手机和电脑上使用相同 URL、key 和账号登录。

## 安全和数据说明
- 只能使用 publishable/anon key，不要把 `service_role` key 放进浏览器。
- SQL 启用了 RLS，并按 `auth.uid() = user_id` 限制行级访问。
- 本地记录不会在未登录时自动上传。首次连接会把本地和云端记录按交易 ID 合并；建议先导出 CSV 备份。
- 当前是可运行的 MVP，不是已部署的公网网站。要在手机和电脑间访问，需要部署到 HTTPS 静态托管（如 Netlify、Vercel 或 Cloudflare Pages）并完成 Supabase 配置。
- 当前盈亏以手动填写的“实际净盈亏”为准；账户权益、回撤和统计基于已录入交易计算，不会连接券商，也不会自动读取行情。
