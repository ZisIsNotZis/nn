[English](README.md) | **简体中文**

<img src="assets/logo.svg" alt="nn" width="200">

# nn

在原生 PyTorch 之上手写神经网络、注意力和训练循环——一份 2021–2022 年的 notebook 归档。

**五十个用完即弃的 Jupyter notebook，从最基础的原语出发重新实现注意力、训练/评估/迁移的脚手架、稀疏 PageRank、图像拟合和 RL 式强化，原样保留下来，作为当初思路推导过程的记录。**

这里没有包、没有入口、没有测试、没有依赖清单。这是一本学习笔记，不是一个库。

## 快速开始

需要装好 Jupyter 和 PyTorch 的 Python 环境。克隆下来，随便打开一个 notebook 读或跑：

```bash
git clone https://github.com/ZisIsNotZis/nn.git
cd nn
jupyter lab attention/2d.ipynb
```

这就是全部受支持的工作流。大多数单元在原始机器之外跑不起来：它们调用 `torch.set_default_tensor_type(torch.cuda.FloatTensor)`，读取刻意没有随仓库发布的图片资源（`assets/`），还依赖原来的绝对路径。整个目录用到的导入有 `torch`、`numpy`、`PIL`、`scipy`、`scikit-learn`、`matplotlib`、`tqdm`、`dash`/`plotly` 和 `rsa`——按你打开的那个 notebook 实际需要装即可。

## 里面有什么

- **从零写注意力** —— [`attention/1dpat.ipynb`](attention/1dpat.ipynb)、[`attention/2d.ipynb`](attention/2d.ipynb)、[`attention/2dpat.ipynb`](attention/2dpat.ipynb)：`Attention`/打分模块，用梯度下降去拟合一张本地图片。
- **自注意力** —— [`SelfAttentionNn.ipynb`](SelfAttentionNn.ipynb)、[`mlpSelfAttention.ipynb`](mlpSelfAttention.ipynb)：一个 `SelfAttentionNn` 模块，在合成的按位解包分类任务上训练。
- **训练/评估/迁移脚手架** —— [`nnMeta/nnTrainerEvaler.ipynb`](nnMeta/nnTrainerEvaler.ipynb)、[`nnMeta/nnTransferer.ipynb`](nnMeta/nnTransferer.ipynb)、`nnMeta/nnTrainEval*.ipynb`、`nnMeta/nnTreeTrainEval*.ipynb`：用 `%run` 串起来的一整个系列的实验宿主，数据来自 `sklearn.datasets.make_classification`。
- **CIFAR-100 上的 CNN** —— [`nnMeta/cnnTrainEval.ipynb`](nnMeta/cnnTrainEval.ipynb)：`ConvBn`/`IterPool` 堆出来的网络，数据是本地 CIFAR-100 pickle 目录。
- **把强化当反传** —— [`reinforcer.ipynb`](reinforcer.ipynb)：一个 `@reinforce` 装饰器，把普通函数（加法、模 16 乘法）变成可学习的模块，并把结果画出来。
- **稀疏 PageRank** —— [`sparsePagerank.ipynb`](sparsePagerank.ipynb)：在 100 万节点的 `scipy.sparse.coo_matrix` 上做幂迭代，行归一化那步用线程池。
- **梯度拟合图像** —— [`imcopy.ipynb`](imcopy.ipynb) 及其副本：先让低分辨率张量拟合目标图，再用 `LANCZOS` 逐级放大；[`Untitled4.ipynb`](Untitled4.ipynb) 则直接硬拟合一个 1080p 张量。
- **小 Dash 应用** —— [`dash.ipynb`](dash.ipynb)、[`dash-Copy1.ipynb`](dash-Copy1.ipynb)：一个键值表编辑器和一个排名演示，写于 Dash 2.0 之前，用的是旧的 `dash_core_components` 导入方式。
- **杂项** —— `Untitled*.ipynb`、`*-CopyN.ipynb`、`*.old.ipynb`、`testDebug.py`、`testDebug*.ipynb`：算术涂鸦、计时和死胡同，没有清理、原样留着。`kv.json` 是它们随手用的键值测试数据。

## 目录结构

```
.
├── attention/           把注意力/模式模块拟合到图片上
├── nnMeta/              训练/评估/迁移脚手架，以及 CIFAR-100 的 CNN
├── docs/project-status.md  分类、证据、边界说明
├── *.ipynb               自注意力、强化、PageRank、Dash、草稿
├── testDebug.py          唯一的 .py 文件：八行算术
└── kv.json               Dash 键值 notebook 用的测试数据
```

每个 notebook 都是独立、平铺的——彼此之间不 import，也没有共享模块。它们之间唯一的"通信"是反复出现的同一套思路：建在 `torch.nn` 上的 `Nn`/`Module`、`Adam` + `OneCycleLR` 的训练循环、以及结尾一个画图的单元。`nnMeta` 那一系列是在前一个 notebook 的脚手架上只改一处再存一份；这种血缘关系正是归档的意义所在，而不是一个半途放弃的重构。

## 开发方式

没有东西需要构建、安装或 lint，也没有测试可跑：目录里没有包元数据、没有 CI 配置、没有依赖清单。当初的做法是：

1. 打开一个 notebook，和它 fork 自的那个并排放着。
2. 就地改模块或任务（通常是改 loss、改 scheduler，或者改样本形状）。
3. 跑训练循环，看图，有意思就留下这个文件。

新的工作不在这里追踪——归档已经冻结、也不再验证；每一簇文件当初是什么、边界在哪里，见 [`docs/project-status.md`](docs/project-status.md)。

## 参与

欢迎修正失效链接、脱敏遗漏或文档事实错误——开 issue 或提 PR，改动越小越好，只要能把这处错误修对。请不要提交 notebook 重构、重排版或新实验；这个目录的价值就在于旧单元保持原样。

如果你 fork 或转发，**请先自己扫一遍**，并阅读下面的脱敏说明。

## 路线图

**已实现** —— "里面有什么"里列的每一项，以 notebook 形式存在。其中几个想法是完整做完的：`SelfAttentionNn.ipynb` 把注意力端到端训练起来了，`sparsePagerank.ipynb` 在百万节点图上收敛了，`reinforcer.ipynb` 两个玩具任务都学会了。

**计划中** —— 没有。这是一份已经关账的归档，不是在建的项目；不会把某个 notebook 提升成库、不会统一到单一入口，也不会移植到当前版本的 PyTorch。现实中的未来就是继续只读地放着：让这些 notebook 留作一份记录——在伸手去拿框架之前，这些东西是怎么一行行手写出来的。后续工作会放在别的仓库里。

## 脱敏说明

这个目录是从一个私有归档里迁移出来的。发布前删除或替换了以下内容：

- 一段硬编码的 RSA 私钥 PEM（现为 `<REDACTED:rsa-private-key>` 占位符）、与之配对的公钥，以及把它写盘的那个单元；
- `cov.ipynb`，其中硬编码了某个私有时间序列后端的 API token、endpoint、org、bucket、设备标识和传感器字段名——整个 notebook 属于雇主内部资产，因此整体删除而不是替换；
- `dawn.yml`，一份内部应用/租户 schema；
- `Untitled1.ipynb` 里雇主内部的工业传感器 tag 列表和对应的 MQTT mock 发布单元，以及 `d:/bq/mqttmock/a.npz` 这个路径；
- 原机器的绝对路径（`D:/my/...`、`d:/a.png`、`d:/prv.pem`），替换为中性占位符；
- `nnMeta/cnnTrainEval.ipynb` 会重新导出的 CIFAR-100 派生目录（本来就不属于这个目录）。

据目前所知，这里不再残留任何凭据、token、私钥、主机名或个人信息。

## 许可证

AGPL-3.0-only，见 [`LICENSE`](LICENSE)。版权所有 ZisIsNotZis。
