# misaka-ning

公开项目主要覆盖 **C++ / Qt 桌面应用、计算机视觉工程、模型实验与边缘部署验证**：从界面与异步任务、本地服务，到数据审核、统一评估和发布检查。下面的三个项目提供可直接查看的实现与验证证据。

## [Vision Studio](https://github.com/misaka-ning/vision-studio) · 本地视觉模型工作台

- **解决的问题：** 在本机完成 YOLO 检测预览、单目标类评估、阈值选择、模型查看与格式转换。
- **项目工程：** 基于 C++17 / Qt 6.8 实现模型与输入会话、异步检测及取消/关闭协调、结果保存、评估配置与报告管理。
- **依赖边界：** Qt 提供界面与线程基础；推理复用 OpenCV DNN、ONNX Runtime、PyTorch / Ultralytics，模型结构图由 Netron 提供。
- **完成状态：** 已发布 Linux 2.10.1 与 Windows 2.9.1。主线 Linux 核心 CI 已通过；Windows 2.10.1 与实体摄像头未验收。核心 CI 与完整发行验收的范围分别见下方记录。

[界面截图与来源](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/docs/releases/evidence/2.10.1/final-visual-review/README.md) · [Linux 发布与下载](https://github.com/misaka-ning/vision-studio/releases/tag/v2.10.1) · [Windows 发布与下载](https://github.com/misaka-ning/vision-studio/releases/tag/v2.9.1)

**核心源码：** [检测调度](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/src/app/detectioncontroller.cpp) · [结果交付](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/src/app/resultdeliveryservice.cpp) · [评估控制](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/src/app/evaluationcontroller.cpp)

**验证入口：** [已通过的主线 CI](https://github.com/misaka-ning/vision-studio/actions/runs/41406483478) · [CI 覆盖范围](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/docs/ci/linux-core.md) · [2.10.1 发布验收记录](https://github.com/misaka-ning/vision-studio/blob/b5849b6add4bf78d9bad506ddebcecc7bcd26bc6/docs/releases/evidence/2.10.1/README.md)

## [SoccerVision-Lab](https://github.com/misaka-ning/SoccerVision-Lab) · 机器人足球视觉实验

- **解决的问题：** 研究小球、遮挡、模糊及无球场景中，检测召回、误报代价与边缘端延迟之间的取舍。
- **项目工程：** C++ / Qt 数据审核工具；Python 实验编排、输入来源校验、统一评估与分场景指标；Jetson Orin NX 上的 TensorRT 推理链路试验。
- **依赖边界：** 检测与训练基于 Ultralytics YOLO26，蒸馏调用所用 Ultralytics 实现的原生能力；项目负责实验配置、对照设计、审计和测量，部署复用 TensorRT / CUDA。
- **完成状态：** 已公开阶段报告、开发 Val 结果与部署试验记录。E08 无蒸馏对照已完成实现和工程验证，正式训练及新指标仍为 `not_run`；现有模型结果为单 seed 开发集记录，部分完整 run 未公开，不能据此宣称独立测试集泛化或生产长稳通过。

[结果与比较口径](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/benchmarks/RESULTS.md) · [Orin NX 同期性能试验](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/experiments/E04_tensorrt_pipeline/PERFORMANCE_COMPARISON.md)

**核心源码：** [数据审核与存储](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/script/dataset-reviewer/src/dataset_store.cpp) · [统一评估入口](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/script/model-evaluation/evaluate.py) · [E08 对照编排](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/experiments/E08_warmstart_no_distillation/e08.py)

**验证入口：** [E08 已归档的工程验证](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/experiments/E08_warmstart_no_distillation/VALIDATION.md) · [复现前提与命令](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/docs/REPRODUCIBILITY.md) · [证据缺口](https://github.com/misaka-ning/SoccerVision-Lab/blob/cd2ed6b1143d536301b8d3feec735b339779e65d/docs/SOURCE_AUDIT.md)

## [MusicPlayer](https://github.com/misaka-ning/Qt-Project---MusicPlayer) · 桌面音乐播放器

- **解决的问题：** 将本地音乐播放、歌词同步、播放列表和可选的云音乐搜索/登录接入桌面界面。
- **项目工程：** C++17 / Qt 6.8 客户端实现播放控制、LRC 解析与定位、列表持久化；Python 本地服务处理云接口、会话保存和错误响应。
- **依赖边界：** 界面和音频播放依赖 Qt Widgets / Multimedia，HTTP 服务基于 FastAPI，部分云接口调用 pyncm，播放与云平台能力来自上述组件和上游服务。
- **完成状态：** 已提供源码与历史本地播放演示，尚无 GitHub Release。Linux CI 的 Release 构建、offscreen 启动/资源测试及 Python 3.9/3.12 离线后端测试通过；该 CI 不验证真实音频设备、上游登录或 Windows/macOS GUI。

[本地播放演示（历史视频）](https://www.bilibili.com/video/BV1tMwCz9ELE/) · [现有功能](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/docs/features.md)

**核心源码：** [播放控制](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/src/player/playercontroller.cpp) · [歌词解析](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/src/player/lrcparser.cpp) · [本地后端](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/python/server/main.py)

**验证入口：** [已通过的主线 CI](https://github.com/misaka-ning/Qt-Project---MusicPlayer/actions/runs/41406217920) · [测试代码](https://github.com/misaka-ning/Qt-Project---MusicPlayer/tree/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/tests) · [构建与验证说明](https://github.com/misaka-ning/Qt-Project---MusicPlayer/blob/a4c195c3c79cb6c7579d4bc7f5bb406468900ef5/docs/development.md)

---

项目状态核查于 **2026-11-03**。源码与报告链接固定到本次核查的主线提交；后续进展可从项目标题进入仓库查看。

<details>
<summary>GitHub 活动统计</summary>

![misaka-ning 的 GitHub 活动统计](./profile/stats.svg)

</details>
