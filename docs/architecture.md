# Architecture

## Two lanes, one radar

AI Daily Radar 不把所有来源混进同一个抓取任务，而是保留两个独立 lane。

### Lane A — Follow Builders

目标是高信号：追踪 builder 的原创帖子、播客和官方博客。主要风险不是“资讯太少”，而是 feed 新鲜度、跨日重复和中央抓取偶发漏项。因此额外加入：

- 每次运行先同步上游；
- feed freshness 检查；
- Podcast 连续两天为 0 才触发原始源兜底；
- 跨日报 episode 去重；
- 不把抓取异常写成“今天没人更新”。

### Lane B — AIHOT

目标是广覆盖：尽量建立过去 24 小时公开 AI 事件集合。主要风险是“局部可见被误认为全量”。因此加入：

- REST cursor 完整链；
- 网页真实 next-link fallback；
- Pass 2 连续性复核；
- A/B/C 覆盖等级（A 仅表示 queried public pool/window 的分页完整性）；
- Hot Topics / Story / Daily 作为编辑层和查漏层，而不是重复计数。

## Why separate schedules

两个任务独立运行，可以分别判断自己的数据质量；失败时也能明确知道是哪一条链路有问题。默认 08:00 + 08:10 还降低了同时访问上游的冲突，并给 08:00 发布的日更源留出刷新缓冲。

## Optional synthesis

如果需要一份最终总览，建议在两份日报都生成之后再做第三步：

1. 对两份日报按事件去重；
2. 标记“builder 一手信号”“广域资讯确认”“两边均出现”；
3. 只输出 3–5 条跨源判断；
4. 不改变原两份日报各自的覆盖等级。
