# SpongeBob-Pro

一个面向中文场景的 MiniLLM 实验仓库，包含：
- 模型定义（`model/`）
- 数据集与预处理（`dataset/`、`data/`）
- 训练脚本（`train/`，含 pretrain / sft / grpo）
- 推理与对话（`eval.py`）
- 基准评测（`benchmark/`）

## 项目结构

```text
SpongeBob-Pro/
|- model/                  # 模型结构与配置
|- dataset/                # 数据集封装与预处理脚本
|- train/                  # 训练脚本（pretrain/sft/grpo）
|- benchmark/              # 评测与测试脚本
|- tokenizer_15k/          # 分词器文件
|- eval.py                 # 交互式推理入口
`- README.md
```

## 环境准备

建议使用 Python 3.10+。

```bash
pip install torch transformers
```

如果你在训练或评测中用到了其他依赖，请按报错补充安装。

## 快速开始：本地对话推理

`eval.py` 支持两种模式：
- `pretrain`：文本续写
- `sft`：对话模式（可单轮/多轮）

示例（SFT，多轮对话）：

```bash
python eval.py ^
  --model_path "你的模型权重路径.pth" ^
  --tokenizer_path "./tokenizer_15k" ^
  --model_type sft ^
  --hidden_size 768 ^
  --num_hidden_layers 12 ^
  --multi_turn
```

示例（Pretrain，文本续写）：

```bash
python eval.py --model_path "你的模型权重路径.pth" --model_type pretrain
```

退出对话可输入：`exit` / `quit` / `退出`。

## 训练与数据

- 训练脚本位于 `train/`：
  - `pretrain.py`
  - `train_sft.py`
  - `train_grpo.py`
- 数据处理脚本位于 `dataset/`，可按你的数据格式进行扩展。

建议先阅读各脚本参数（`-h`）再启动训练：

```bash
python train/train_sft.py -h
python train/pretrain.py -h
python train/train_grpo.py -h
```

## 评测

评测相关脚本位于 `benchmark/`，例如：
- `benchmark/evaluator.py`
- `benchmark/mini_bench/run_test.py`
- `benchmark/test_xcopa_improved.py`

你可以按任务类型修改数据路径和模型路径后运行。

## 你可以继续定制的部分

- 把“模型权重下载方式/链接”补到 README
- 增加你当前最常用的一键命令（训练、推理、评测）
- 增加实验记录（数据版本、超参、指标）

---

如果你愿意，我可以下一步再帮你把 README 升级成“论文风格”版本（加实验结果表、TODO、Roadmap、徽章与更新日志）。
