# 嗨，我是 misaka-ning 👋

**主要做计算机视觉和边缘部署，也喜欢写算法题和做一些C++ Qt小项目。**

关注模型从实验环境走到实际设备的过程：数据是否可靠、指标如何比较、推理延迟花在哪里，以及模型接进应用之后能不能稳定工作。

这个 GitHub 放着视觉实验、桌面工具和一些沿途写下的记录。可以从下面三个项目开始逛。

---

### ⚽ [SoccerVision-Lab](https://github.com/misaka-ning/SoccerVision-Lab)

**让机器人找到足球，也学会在没有球的时候别乱报。**

球场给检测模型出的题不少：目标小、遮挡多、运动时画面模糊，还要在边缘设备上及时给出结果。模型能找到多少球、会认错多少次、跑一帧需要多久，这些问题需要一起看。

这个仓库记录了围绕机器人足球视觉的一系列工作：

- 用 C++ / Qt 工具审核数据，检查标注与样本。
- 基于 Ultralytics YOLO 开展微调、蒸馏与对照实验。
- 使用统一评估流程，观察召回、误报和不同场景下的表现。
- 在 Jetson Orin NX 上尝试 TensorRT 推理，测量实际部署中的性能。

实验里有效的结果和没起作用的尝试都保留下来。E08 对照尚未正式训练，已有结果的比较条件与局限也写在文档中。

[技术阅读入口](https://github.com/misaka-ning/SoccerVision-Lab/blob/main/docs/TECHNICAL_READING.md) · [实验结果](https://github.com/misaka-ning/SoccerVision-Lab/blob/main/benchmarks/RESULTS.md) · [复现说明](https://github.com/misaka-ning/SoccerVision-Lab/blob/main/docs/REPRODUCIBILITY.md)

`Python` · `YOLO` · `TensorRT` · `CUDA` · `Jetson Orin NX`

### 🖥️ [Vision Studio](https://github.com/misaka-ning/vision-studio)

**给视觉模型一个桌面工作台。**

加载模型、预览检测、比较评估结果、选择阈值，再查看模型结构或转换格式，把这些操作放进同一个应用里。

模型之外，这个项目也关心桌面软件里的具体问题：

- 推理进行时，界面怎样保持响应？
- 用户取消任务之后，已经在路上的结果该怎么处理？
- 输入速度超过处理速度时，结果如何交付？
- 关闭窗口时，线程和本地服务怎样妥善退出？

按钮上只有两个字的“取消”，实现起来往往不止两行。

推理与模型能力复用 OpenCV DNN、ONNX Runtime、PyTorch / Ultralytics 等组件；仓库中的工作主要围绕桌面交互、任务协调、评估流程和应用集成展开。

[查看项目](https://github.com/misaka-ning/vision-studio) · [发布与下载](https://github.com/misaka-ning/vision-studio/releases) · [构建与回归检查](https://github.com/misaka-ning/vision-studio/actions)

`C++17` · `Qt 6.8` · `ONNX Runtime` · `OpenCV`

### 🎵 [MusicPlayer](https://github.com/misaka-ning/Qt-Project---MusicPlayer)

**从播放一首歌开始，处理好一个桌面应用的日常。**

一个基于 Qt 的音乐播放器，包含本地播放、同步歌词、播放列表，以及可选的云音乐搜索与登录功能。

播放控制、歌词解析和列表持久化由 C++ / Qt 客户端处理，云接口通过 Python 本地服务接入。项目也涉及不少容易被忽略的小事：拖动进度后歌词能否跟上、重启后列表是否还在、后端请求失败时界面如何回应。

[本地播放演示](https://www.bilibili.com/video/BV1tMwCz9ELE/) · [功能说明](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/main/docs/features.md) · [构建与开发](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/main/docs/development.md)

`C++17` · `Qt Widgets / Multimedia` · `Python` · `FastAPI`

---

### 🔎 接下来想继续深入的方向

- **视觉模型评估**：理解指标背后的样本、阈值和使用场景。
- **边缘推理优化**：关注延迟、吞吐、资源占用，以及完整处理流程的开销。
- **C++ 应用集成**：把推理能力接进交互清晰、运行稳定的工具。
- **可复现的工程实践**：让下一次实验，以及下一位读代码的人，都更容易接着往下做。

欢迎围绕这些方向交流，也欢迎在项目里留下具体问题。

### ☕ README 的休息区

几个适合等编译时想的问题：

- 进度条从 99% 走到 100%，为什么总像一段独立的人生？
- 文件叫 `final_v3_really_final` 时，下一版应该叫什么？
- 如果机器人踢出了界外球，它会认为是自己的问题，还是球场太小？

<details>
<summary>这里还有一位临时访客 🐈</summary>

```text
 /\_/\
( o.o )   正在观察光标。
 > ^ <
```

它暂时没有提交代码，但已经占据了 README 的一部分。

</details>

<details>
<summary>技术细节与验证</summary>

以下保留 2026-11-03 核查时的源码、结果和验证记录，链接固定到当时的提交；最新进展见各项目仓库。

**Vision Studio**

[Vision Studio](https://github.com/misaka-ning/vision-studio) · 本地视觉模型工作台

[界面截图与来源](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/docs/releases/evidence/2.10.1/final-visual-review/README.md) · [Linux 发布与下载](https://github.com/misaka-ning/vision-studio/releases/tag/v2.10.1) · [Windows 发布与下载](https://github.com/misaka-ning/vision-studio/releases/tag/v2.9.1)

**核心源码：** [检测调度](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/src/app/detectioncontroller.cpp) · [结果交付](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/src/app/resultdeliveryservice.cpp) · [评估控制](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/src/app/evaluationcontroller.cpp)

**验证入口：** [已通过的主线 CI](https://github.com/misaka-ning/vision-studio/actions/runs/41406483478) · [CI 覆盖范围](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/docs/ci/linux-core.md) · [2.10.1 发布验收记录](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/docs/releases/evidence/2.10.1/README.md)

**SoccerVision-Lab**

[SoccerVision-Lab](https://github.com/misaka-ning/SoccerVision-Lab) · 机器人足球视觉实验

[结果与比较口径](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/benchmarks/RESULTS.md) · [Orin NX 同期性能试验](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/experiments/E04_tensorrt_pipeline/PERFORMANCE_COMPARISON.md)

**核心源码：** [数据审核与存储](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/script/dataset-reviewer/src/dataset_store.cpp) · [统一评估入口](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/script/model-evaluation/evaluate.py) · [E08 对照编排](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/experiments/E08_warmstart_no_distillation/e08.py)

**验证入口：** [E08 已归档的工程验证](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/experiments/E08_warmstart_no_distillation/VALIDATION.md) · [复现前提与命令](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/docs/REPRODUCIBILITY.md) · [证据缺口](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/docs/SOURCE_AUDIT.md)

**MusicPlayer**

[MusicPlayer](https://github.com/misaka-ning/Qt-Project---MusicPlayer) · 桌面音乐播放器

[本地播放演示（历史视频）](https://www.bilibili.com/video/BV1tMwCz9ELE/) · [现有功能](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/docs/features.md)

**核心源码：** [播放控制](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/src/player/playercontroller.cpp) · [歌词解析](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/src/player/lrcparser.cpp) · [本地后端](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/python/server/main.py)

**验证入口：** [已通过的主线 CI](https://github.com/misaka-ning/Qt-Project---MusicPlayer/actions/runs/41406217920) · [测试代码](https://github.com/misaka-ning/Qt-Project---MusicPlayer/tree/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/tests) · [构建与验证说明](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/docs/development.md)

</details>

<details>
<summary>GitHub 活动统计</summary>

![misaka-ning 的 GitHub 活动统计](./profile/stats.svg)

</details>
