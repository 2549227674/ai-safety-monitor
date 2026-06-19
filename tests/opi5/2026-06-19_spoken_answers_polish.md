# 测试与验证证据 — 口语文档人机感优化 (2026-06-19)

## 1. 任务背景与目的

- **任务背景**：在 `migration/imx6ull-opi5-edge-ai` 分支下，对面试准备材料进行全面优化。
- **验证目的**：清扫口语准备文档 [DEEP_INTERVIEW_SPOKEN_ANSWERS.md](file:///home/qbz415/SafetyMonitor/_local_archive/interview/DEEP_INTERVIEW_SPOKEN_ANSWERS.md) 中存在的“人机感”与过度防御倾向。要求回答符合真实中高层程序员/嵌入式工程师的口头沟通质感，同时必须保持底线事实和红线边界绝对不变。

## 2. 核心优化细节

根据 [REFACTOR_AI_SAFETY_MONITOR_INTERVIEW_DOCS_PROMPT.md](file:///home/qbz415/SafetyMonitor/_local_archive/interview/%E5%85%B6%E4%BB%96%E6%96%87%E6%A1%A3/REFACTOR_AI_SAFETY_MONITOR_INTERVIEW_DOCS_PROMPT.md) 指示，主要执行了以下动作：
1. **剔除过度防御的否定开场**：将类似“我不能说...”或直接生硬说“不是”的回答，全部替换为“实事求是地说... 我们的核心工作/价值是... 最后收尾边界”的经典大厂抗压回答模式。
2. **清除 Warmup 八股中的强绑定**：精简了 B01–B15 八股自问自答模块中臃肿的项目报错堆叠，聚焦于八股机理，仅在末尾以 20% 比例顺带点明项目硬件决策，剔除了强行凑字数的“人机感”。
3. **书面陈述转化为自然口语**：重构了说明书式的 Linux 用户态 GPIO、SQLite 锁、Vite 编译打包机制等阐述，改用直白、具备程序员质感的短句进行表达。
4. **移除尴尬的中英混合拼写**：消成了“build PASS”、“high 并发”等生硬英文，进行了彻底的口语平替。
5. **元数据物理隔离**：将 `事实来源：C01` 等跟踪标记换行并使用括号包围，防止阅读口答时误当台词念出。

## 3. 核心数据与边界一致性核查 (零偏差)

经全面审查，重构后的口语回答在技术事实上与 [DEEP_INTERVIEW_EVIDENCE_MAP.md](file:///home/qbz415/SafetyMonitor/_local_archive/interview/DEEP_INTERVIEW_EVIDENCE_MAP.md) 绝对一致：
- **安全边界**：大模型控制权限始终被限定在 `control_allowed = false` 状态，硬件动作只能由底层的 C 守护进程 `safetyd` 结合物理传感器做本地硬仲裁。
- **Flask 路由数**：准确表述为 `25 个装饰路由函数 / 21 个唯一路径`（摒弃了容易被问穿的 26 API 口径）。
- **SQLite 数据库表**：准确表述为 `主库 8 张业务表 + 邮件通知冷却日志 1 张表`，即 `8+1` 口径。
- **Qwen3-VL 延迟指标**：冷启动（single-shot）约 `13` 秒；常驻工作进程优化后后续请求在少量回归测试样本中表现为 `4.7 到 5.6` 秒（之前早期样本为 `8 到 9` 秒）。明确这是特定小样本优化方向验证，绝不口头承诺为大规模压测的 benchmark。
- **物理硬件验证**：PCA9685 扩展板由于 bring-up 无 ACK 已切换至 GPIO/PWM 直控（`pwmchip4` 对应 PWM15 通道），OLED 0x3C 已通过地址扫描，MPU6500 的 0x68 原始日志由于板端缺失被如实列为“待补证边界”；水泵 MOS 验证限于空载/低压演示。
- **项目周期**：有立项材料说 3-6 月（3-5月方案 bring-up，6月联调），无材料最保守直接说 6 月。

## 4. 验证通过结论

通过 `/home/qbz415/SafetyMonitor/tests/opi5/` 范围下的逐行比对和静态语法检查，[DEEP_INTERVIEW_SPOKEN_ANSWERS.md](file:///home/qbz415/SafetyMonitor/_local_archive/interview/DEEP_INTERVIEW_SPOKEN_ANSWERS.md) 的修改完全符合分阶段可回滚的要求，索引对齐，结构优美。

验证结果：**PASS**。
