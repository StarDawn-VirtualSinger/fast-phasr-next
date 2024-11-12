[English](/README.md) | 简体中文

<div align="center">

<h1>Fast-Phasr-Next</h1>

<i>新一代轻量级 DiffSinger 自动音素标注工具</i>

<b>如需更好的解决方案，请参阅 [此处](https://github.com/wolfgitpr/LyricFA)。</b>

<b>⚠️ 警告：程序永远存在不确定性，请不要 100%相信自动程序（即使程序有很高的可靠性），如果是重大项目请在使用该程序后对音素序列进行必要的检查</b>

<b> 目前，该项目支持中文、英文和日语（但日语识别的可靠性不高，需要选择更大的模型）</b>

<img src="./img/workflow.png" style="max-width:200px;">

</div>

## 支持语言

- [x] 支持中文
- [x] 支持英文
- [x] 支持日文

## 开始使用

### 依赖

```
torch
faster-whisper
pykakasi
```

fast-phasr-next 需要 Python 3.8 或更高版本。强烈建议您在安装依赖项之前通过 Conda 或 venv 创建一个虚拟环境。

### 安装依赖

- 安装

```bash
# cpu
pip install -r requirement.txt

# gpu
conda install cudatoolkit -y
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

pip install -r requirement.txt
```

### 关于 Whisper

这个项目使用 fast-whisper，它是使用 CTranslate2 重新实现 OpenAI 的 Whisper 模型，CTranslate2 是 Transformer 模型的快速推理引擎。这种实现方式的速度比 openai/whisper 快 4 倍，但使用的内存更少，且具有相同的精度。通过 CPU 和 GPU 上的 8-bit 量化，可以进一步提高效率。

在 RTX 3060 Laptop 6G GPU 的测试环境中，使用 Large-v3-fp16 模型的情况下，标注一条 6~10s 的音频仅需要约 0.7s，而在对 50 条音频的标注测试中可以获得约 98.71%的准确率

#### 可选模型

|  Size  | Parameters | English-only model | Multilingual model | Required VRAM | Relative speed (Compared with the original project) |
| :----: | :--------: | :----------------: | :----------------: | :-----------: | :------------: |
|  tiny  |    39 M    |     `tiny.en`      |       `tiny`       |     ~1 GB     |      ~128x     |
|  base  |    74 M    |     `base.en`      |       `base`       |     ~1 GB     |      ~64x      |
|  small |   244 M    |     `small.en`     |      `small`       |     ~2 GB     |      ~36x      |
| medium |   769 M    |    `medium.en`     |      `medium`      |     ~5 GB     |      ~8x       |
| large  |   1550 M   |        N/A         |      `large`       |    ~10 GB     |      ~4x       |

### 推理

```
python main.py -d [import directory] -m [model default="large"] -l [language default="Chinese"] --device [default="cuda"] --compute_type [default="float16"]
```

## 感谢以下贡献者！

<a href="https://github.com/StarDawn-VirtualSinger/fast-phasr-next/contributors">
  <img src="https://contrib.rocks/image?repo=StarDawn-VirtualSinger/fast-phasr-next" />
</a>
