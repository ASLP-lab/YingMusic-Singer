<div align="center">

<h1>🎤 YingMusic-Singer-Plus：具备灵活歌词编辑与免标注旋律引导的可控歌声合成</h1>

<img src="assets/model_logo.gif" width="61.8%">

<p>
  <a href="">English</a> ｜ <a href="README_ZH.md">中文</a>
</p>


![Python](https://img.shields.io/badge/Python-3.10-3776AB?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-CC--BY--4.0-lightgrey)

[![arXiv Paper](https://img.shields.io/badge/arXiv-2603.24589-b31b1b?logo=arxiv&logoColor=white)](https://arxiv.org/abs/2603.24589)
[![GitHub](https://img.shields.io/badge/GitHub-YingMusic--Singer-181717?logo=github&logoColor=white)](https://github.com/ASLP-lab/YingMusic-Singer-Plus)
[![Demo Page](https://img.shields.io/badge/GitHub-Demo--Page-8A2BE2?logo=github&logoColor=white&labelColor=181717)](https://aslp-lab.github.io/YingMusic-Singer-Plus-Demo/)
[![HuggingFace Space](https://img.shields.io/badge/🤗%20HuggingFace-Space-FFD21E)](https://huggingface.co/spaces/ASLP-lab/YingMusic-Singer-Plus)
[![HuggingFace Model](https://img.shields.io/badge/🤗%20HuggingFace-Model-FF9D00)](https://huggingface.co/ASLP-lab/YingMusic-Singer-Plus)
[![Dataset LyricEditBench](https://img.shields.io/badge/🤗%20HuggingFace-LyricEditBench-FF6F00)](https://huggingface.co/datasets/ASLP-lab/LyricEditBench)
[![Discord](https://img.shields.io/badge/Discord-Join%20Us-5865F2?logo=discord&logoColor=white)](https://discord.gg/RXghgWyvrn)
[![WeChat](https://img.shields.io/badge/WeChat-Group-07C160?logo=wechat&logoColor=white)](https://github.com/ASLP-lab/YingMusic-Singer-Plus/blob/main/assets/wechat_qr.png)
[![Lab](https://img.shields.io/badge/🏫%20ASLP-Lab-4A90D9)](http://www.npu-aslp.org/)

<p>
        <a href="https://orcid.org/0009-0005-5957-8936">郝春博</a><sup>1,2</sup> ·
        <a href="https://orcid.org/0009-0003-2602-2910">郑俊杰</a><sup>2</sup> ·
        <a href="https://orcid.org/0009-0001-6706-0572">马国斌</a><sup>1</sup> ·
        姜月鹏<sup>1</sup> ·
        陈华康<sup>1</sup> ·
        田文杰<sup>1</sup> ·
        <a href="https://orcid.org/0009-0003-9258-4006">陈宫煜</a><sup>2</sup> ·
        <a href="https://orcid.org/0009-0005-5413-6725">陈子浩</a><sup>2</sup> ·
        谢磊<sup>1</sup>
</p>

<p>
        <sup>1</sup> 西北工业大学计算机学院，音频、语音与语言处理研究组 (ASLP@NPU)<br>
        <sup>2</sup> 巨人网络，AI实验室
</p>

</div>

## 🎥 演示视频

点击下方徽章跳转观看演示视频：

| YouTube | Bilibili |
|---------|----------|
| [![YouTube](assets/YingMusic-Singer-Plus.png)](https://www.youtube.com/watch?v=ktjJFS5R3Dk) | [![Bilibili](assets/YingMusic-Singer-Plus.png)](https://www.bilibili.com/video/BV1zPDSBhEkz/) |

## 📖 简介

**YingMusic-Singer-Plus** 是一个完全基于扩散模型的歌声合成模型，能够实现**旋律可控的歌声编辑与灵活的歌词操作**，无需人工对齐或精确的音素标注。

仅需三个输入——一个可选的音色参考、一个提供旋律的演唱片段以及修改后的歌词——YingMusic-Singer-Plus 即可合成**44.1 kHz** 的高保真歌声，并忠实地保留原始旋律。

<div align="center">
<img src="./assets/YingMusic-Singer.drawio.svg" alt="YingMusic-Singer-Plus 架构" width="90%">
<p><i>YingMusic-Singer-Plus 的整体架构。左：SFT 训练流程。右：GRPO 训练流程。</i></p>
</div>

## ✨ 核心特性

- **免标注**：推理时无需人工歌词-MIDI对齐
- **灵活的歌词操作**：支持6种编辑类型——部分/全部更改、插入、删除、翻译（中↔英）和中英混
- **强旋律保持**：基于CKA的旋律对齐损失 + 基于GRPO的优化
- **双语支持**：统一的中英文IPA分词器
- **高保真度**：通过 Stable Audio 2 VAE 实现 44.1 kHz 立体声输出

## 🚀 快速开始

### 选项1：从零开始安装

```bash
# 我们强烈推荐使用 uv 以获得更快的依赖解析。
uv venv --python 3.10
source .venv/bin/activate  # Windows: .venv\Scripts\activate
uv pip install -r requirements.txt

# 如果您在中国，可以使用 USTC 镜像加速下载：
uv pip install -r requirements.txt -i https://mirrors.ustc.edu.cn/pypi/simple

# 或者，也支持 conda：
conda create -n YingMusic-Singer-Plus python=3.10
conda activate YingMusic-Singer-Plus
pip install uv
uv pip install -r requirements.txt

# 如果您在中国：
uv pip install -r requirements.txt -i https://mirrors.ustc.edu.cn/pypi/simple
```

### 选项2：预构建环境

**Conda**

1. 从 https://repo.anaconda.com/miniconda/ 为您的平台下载并安装 **Miniconda**。使用 `conda --version` 验证安装。
2. 从下方表格中下载适合您配置的预构建环境包。
3. 导航到您的 Conda `envs/` 目录，创建一个名为 `YingMusic-Singer-Plus` 的文件夹。
4. 将下载的包移动到该文件夹中并解压：
```bash
   tar -xvf <package_name>
```

**uv**

1. 通过 `pip install uv` 安装 **uv**，或遵循[官方说明](https://docs.astral.sh/uv/getting-started/installation/)。
2. 从下方表格中下载适合您配置的预构建环境包。
3. 解压包并激活环境：
```bash
   tar -xvf <package_name>
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
```

| CPU 架构 | GPU    | 操作系统  | 类型   | 下载链接     |
|------------------|--------|---------|-------|--------------|
| AMD64            | NVIDIA | Linux   | Conda | 即将推出      |
| AMD64            | NVIDIA | Linux   | uv    | 即将推出      |
| AMD64            | NVIDIA | Windows | uv    | 即将推出      |

### 选项3：Docker

构建镜像：

```bash
docker build -t YingMusic-Singer-Plus .
```

## 🎵 推理

### 选项1：在线演示（HuggingFace Space）

访问 https://huggingface.co/spaces/ASLP-lab/YingMusic-Singer-Plus ，在浏览器中即时试用模型。

### 选项2：本地 Gradio 应用（与在线演示相同）

```bash
python app_local.py
```

### 选项3：命令行推理

```bash
python infer.py \
    --ref_audio examples/hf_space/melody_control/melody_control_ZH_02_timbre.wav \
    --melody_audio examples/hf_space/melody_control/melody_control_ZH_02_melody.wav \
    --ref_text "就让你|在别人怀里|快乐" \
    --target_text "Missing you in my mind|missing you in my heart" \
    --output output/melody_control_zh_missing_you.wav
```

启用人声分离和伴奏混合：

```bash
python infer.py \
    --ref_audio examples/hf_space/lyric_edit/SingEdit_EN_01.wav \
    --melody_audio examples/hf_space/lyric_edit/SingEdit_EN_01.wav \
    --ref_text "can you tell my heart is speaking|my eyes will give you clues" \
    --target_text "can you spot the moon is grinning|my lips will show you hints" \
    --separate_vocals \
    --mix_accompaniment \
    --output output/lyric_edit_en_moon_grinning.wav
```

### 选项4：批量推理

> **注意**：输入模型的所有音频必须是纯人声轨道（无伴奏）。如果您的输入包含伴奏，请先使用 `src/third_party/MusicSourceSeparationTraining/inference_api.py` 进行人声分离。

输入 JSONL 文件应每行包含一个 JSON 对象，格式如下：

```json
{
    "id": "lyric_edit_en_moon_grinning",
    "melody_ref_path": "examples/hf_space/lyric_edit/SingEdit_EN_01.wav",
    "gen_text": "can you spot the moon is grinning|my lips will show you hints",
    "timbre_ref_path": "examples/hf_space/lyric_edit/SingEdit_EN_01.wav",
    "timbre_ref_text": "can you tell my heart is speaking|my eyes will give you clues"
}
```

```bash
python batch_infer.py \
    --input_type jsonl \
    --input_path /path/to/input.jsonl \
    --output_dir /path/to/output \
    --ckpt_path /path/to/ckpts \
    --num_gpus 4
```

在 **LyricEditBench（旋律控制）** 上进行多进程推理——测试集将自动下载：

```bash
python inference_mp.py \
    --input_type lyric_edit_bench_melody_control \
    --output_dir path/to/LyricEditBench_melody_control \
    --ckpt_path ASLP-lab/YingMusic-Singer-Plus \
    --num_gpus 8
```

在 **LyricEditBench（歌唱编辑）** 上进行多进程推理：

```bash
python inference_mp.py \
    --input_type lyric_edit_bench_sing_edit \
    --output_dir path/to/LyricEditBench_sing_edit \
    --ckpt_path ASLP-lab/YingMusic-Singer-Plus \
    --num_gpus 8
```

## 🏗️ 模型架构

YingMusic-Singer-Plus 由四个核心组件组成：

| 组件 | 描述 |
|-----------|-------------|
| **VAE** | Stable Audio 2 编码器/解码器；将 44.1 kHz 立体声音频下采样 2048 倍 |
| **旋律提取器** | 预训练 MIDI 提取模型 (SOME) 的编码器；捕捉解耦的旋律信息 |
| **IPA 分词器** | 将中英文歌词转换为统一的音素序列，并带有句子级对齐 |
| **基于DiT的CFM** | 遵循 F5-TTS 的条件流匹配主干网络（22 层，16 个头，隐藏维度 1024） |

**总参数量**：约 727.3M (453.6M CFM + 156.1M VAE + 117.6M 旋律提取器)

## 📊 LyricEditBench

我们引入了 **LyricEditBench**，这是首个用于旋律保持型歌词修改评估的基准，基于 [GTSinger](https://github.com/GTSinger/GTSinger) 构建。该数据集可在 HuggingFace 上获取：https://huggingface.co/datasets/ASLP-lab/LyricEditBench 。

### 结果

<div align="center">
<p><i>表 2：与基线模型在 LyricEditBench 上针对表 1 中任务类型和语言的比较。指标 (M)：P: PER，S: SIM，F: F0-CORR，V: VS 详见第 3 节。最佳结果以粗体显示。</p>
<img src="./assets/results.png" alt="LyricEditBench 结果" width="90%">
</div>

## 🙏 致谢

本工作建立在以下开源项目之上：

- [F5-TTS](https://github.com/SWivid/F5-TTS) —— 基于 DiT 的 CFM 主干网络
- [Stable Audio 2](https://github.com/Stability-AI/stable-audio-tools) —— VAE 架构
- [SOME](https://github.com/openvpi/SOME) —— 旋律提取器
- [DiffRhythm](https://github.com/ASLP-lab/DiffRhythm) —— 句子级对齐策略
- [GTSinger](https://github.com/GTSinger/GTSinger) —— 基准基础语料库
- [Emilia](https://huggingface.co/datasets/amphion/Emilia-Dataset) —— TTS 预训练数据

## 📄 许可证

本项目中的代码和模型权重根据 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可，**除了**以下部分：

VAE 模型权重和推理代码（位于 `src/YingMusic-Singer/utils/stable-audio-tools` 中）源自 Stability AI 的 [Stable Audio Open](https://huggingface.co/stabilityai/stable-audio-open-1.0)，并根据 [Stability AI Community License](./LICENSE-STABILITY) 许可。

## ✉️ 联系我们
如果您对我们的工作感兴趣并想留言，欢迎发送邮件至 cbhao@mail.nwpu.edu.cn 或 lxie@nwpu.edu.cn。

欢迎加入我们的微信群进行技术讨论、获取更新。

<p align="center">
  <!-- <em>由于群组限制，如果无法扫描二维码，请添加我的微信以加入群组 -->
      <!-- : <strong>Tiamo James</strong></em> -->
  <br>
  <span style="display: inline-block; margin-right: 10px;">
    <img src="https://github.com/ASLP-lab/YingMusic-Singer-Plus/blob/main/assets/wechat_qr.png" width="300" alt="微信群二维码"/>
  </span>
  <span style="display: inline-block; margin-right: 10px;">
    <img src="https://github.com/ASLP-lab/YingMusic-Singer-Plus/blob/main/assets/wechat_qr_author.png" width="300" alt="微信群二维码"/>
  </span>
</p>

## Star 历史

<a href="https://www.star-history.com/?repos=ASLP-lab%2FYingMusic-Singer-Plus&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/image?repos=ASLP-lab/YingMusic-Singer-Plus&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/image?repos=ASLP-lab/YingMusic-Singer-Plus&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/image?repos=ASLP-lab/YingMusic-Singer-Plus&type=date&legend=top-left" />
 </picture>
</a>

<p align="center">
  <img src="https://raw.githubusercontent.com/ASLP-lab/YingMusic-Singer-Plus/main/assets/institutional_logo.svg" alt="机构徽标" width="600">
</p>
