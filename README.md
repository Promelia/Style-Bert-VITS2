> **Note:** This is an English translation version with some edits. Original repository: [https://github.com/litagin02/Style-Bert-VITS2](https://github.com/litagin02/Style-Bert-VITS2)

# Style-Bert-VITS2

**Please be sure to read the [Terms of Use for Requests and Default Models](/docs/TERMS_OF_USE.md) before using this software.**

Bert-VITS2 with more controllable voice styles.

https://github.com/litagin02/Style-Bert-VITS2/assets/139731664/e853f9a2-db4a-4202-a1dd-56ded3c562a0

You can install via `pip install style-bert-vits2` (inference only), see [library.ipynb](/library.ipynb) for example usage.

- **Tutorial Videos** [YouTube](https://youtu.be/aTUSzgDl1iY) [Niconico Video](https://www.nicovideo.jp/watch/sm43391524)
- [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](http://colab.research.google.com/github/litagin02/Style-Bert-VITS2/blob/master/colab.ipynb)
- [**Frequently Asked Questions** (FAQ)](/docs/FAQ.md)
- [🤗 Online Demo Available Here](https://huggingface.co/spaces/litagin/Style-Bert-VITS2-Editor-Demo)
- [Zenn Article](https://zenn.dev/litagin/articles/034819a5256ff4)

- [**Releases Page**](https://github.com/litagin02/Style-Bert-VITS2/releases/), [Changelog](/docs/CHANGELOG.md)
  - 2025-08-24: Ver 2.7.0: Added ONNX conversion GUI for integration with external libraries such as [Aivis Project](https://aivis-project.com/), and added `litagin/anime-whisper` as a speech recognition model
  - 2024-09-09: Ver 2.6.1: Bug fixes only, including issues with Google Colab training
  - 2024-06-16: Ver 2.6.0 (Added differential model merge, weighted merge, null model merge; see [this article](https://zenn.dev/litagin/articles/1297b1dc7bdc79) for usage)
  - 2024-06-14: Ver 2.5.1 (Changed terms of use to requests only)
  - 2024-06-02: Ver 2.5.0 (**Added [Terms of Use](/docs/TERMS_OF_USE.md)**), added style generation from folder structure, added Kotoha Ami/Amitaro models, and improved installation speed
  - 2024-03-16: ver 2.4.1 (**Changed installation method using bat files**)
  - 2024-03-15: ver 2.4.0 (Large-scale refactoring and various improvements, library support)
  - 2024-02-26: ver 2.3 (Dictionary and editor features)
  - 2024-02-09: ver 2.2
  - 2024-02-07: ver 2.1
  - 2024-02-03: ver 2.0 (JP-Extra)
  - 2024-01-09: ver 1.3
  - 2023-12-31: ver 1.2
  - 2023-12-29: ver 1.1
  - 2023-12-27: ver 1.0

This repository is based on [Bert-VITS2](https://github.com/fishaudio/Bert-VITS2) v2.1 and Japanese-Extra, so many thanks to the original author!

**Overview**

- Based on [Bert-VITS2](https://github.com/fishaudio/Bert-VITS2) v2.1 and Japanese-Extra, which generates emotionally rich voices from input text, this project allows you to freely control emotions and speech styles with varying intensities.
- Even if you're not familiar with Git or Python, you can easily install and train models on Windows (many features borrowed from [EasyBertVits2](https://github.com/Zuntan03/EasyBertVits2/)). Google Colab training is also supported: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](http://colab.research.google.com/github/litagin02/Style-Bert-VITS2/blob/master/colab.ipynb)
- For speech synthesis only, it runs on CPU even without a graphics card.
- For speech synthesis only, you can install it as a Python library with `pip install style-bert-vits2`. See [library.ipynb](/library.ipynb) for examples.
- Includes an API server for integration with other tools (PR by [@darai0512](https://github.com/darai0512), thank you!).
- Bert-VITS2's strength lies in reading happy texts happily and sad texts sadly, so even with default settings, it generates emotionally rich voices.


## Usage

- For CLI usage, see [here](/docs/CLI.md).
- Also see the [Frequently Asked Questions](/docs/FAQ.md).

### System Requirements

We have confirmed operation in Windows Command Prompt, WSL2, and Linux (Ubuntu Desktop) for each UI and API Server (for WSL, please use relative paths and similar workarounds). Without an NVidia GPU, training is not possible, but speech synthesis and merging are available.

### Installation

For pip installation and usage examples as a Python library, see [library.ipynb](/library.ipynb).

#### For Users Unfamiliar with Git and Python

Assuming you're on Windows.

1. Download and extract [this zip file](https://github.com/litagin02/Style-Bert-VITS2/releases/latest/download/sbv2.zip) to a **location that does not contain Japanese characters or spaces in the path**.
  - If you have a graphics card, double-click `Install-Style-Bert-VITS2.bat`.
  - If you don't have a graphics card, double-click `Install-Style-Bert-VITS2-CPU.bat`. The CPU version cannot train models, but speech synthesis and merging are possible.
2. Wait for the necessary environment to be installed automatically.
3. After that, if the speech synthesis editor starts automatically, installation is successful. A default model will be downloaded, so you can start using it right away.

If you want to update, double-click `Update-Style-Bert-VITS2.bat`.

However, if updating from a version before **2.4.1** (2024-03-16), you need to delete everything and reinstall. Sorry for the inconvenience. See [CHANGELOG.md](/docs/CHANGELOG.md) for migration details.

#### For Users Familiar with Git and Python

Since [uv](https://github.com/astral-sh/uv), a Python virtual environment and package management tool, is faster than pip, we recommend using it.
(If you don't want to use it, regular pip is fine.)

```bash
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
git clone https://github.com/litagin02/Style-Bert-VITS2.git
cd Style-Bert-VITS2
uv venv venv
venv\Scripts\activate
uv pip install "torch<2.4" "torchaudio<2.4" --index-url https://download.pytorch.org/whl/cu118
uv pip install -r requirements.txt
python initialize.py  # Download necessary models and default TTS model
```
Don't forget the last step.

### Speech Synthesis

The speech synthesis editor can be started by double-clicking `Editor.bat` or running `python server_editor.py --inbrowser` (use `--device cpu` to start in CPU mode). Within the interface, you can create scripts by changing settings for each line, save and load, and edit dictionaries.
The default model is downloaded during installation, so you can use it even without training.

The editor portion is in a [separate repository](https://github.com/litagin02/Style-Bert-VITS2-Editor).

For speech synthesis WebUI in versions 2.2 and earlier, double-click `App.bat` or run `python app.py` to start the WebUI. Or double-click `Inference.bat` to open just the speech synthesis tab.

The structure of model files required for speech synthesis is as follows (no manual placement is necessary):
```
model_assets
├── your_model
│   ├── config.json
│   ├── your_model_file1.safetensors
│   ├── your_model_file2.safetensors
│   ├── ...
│   └── style_vectors.npy
└── another_model
    ├── ...
```
As shown, inference requires `config.json`, `*.safetensors`, and `style_vectors.npy`. When sharing models, share these three files.

Among these, `style_vectors.npy` is the file needed to control styles. During training, the default average style "Neutral" is generated by default.
For those who want to control styles in more detail using multiple styles, see the "Style Generation" section below (even with just the average style, if the training data is emotionally rich, you can generate sufficiently emotionally rich voices).

### Training

- For detailed training instructions via CLI, see [here](docs/CLI.md).
- For detailed training on Paperspace, see [here](docs/paperspace.md). For training on Colab, see [here](http://colab.research.google.com/github/litagin02/Style-Bert-VITS2/blob/master/colab.ipynb).

Training requires multiple audio files of approximately 2-14 seconds and their transcription data.

- If you already have pre-split audio files and transcription data from existing corpora, you can use them as-is (modifying transcription files as needed). See "Training WebUI" below.
- If not, if you only have audio files (any length), we have included a tool to create a dataset ready for training.

#### Creating a Dataset

- From the "Dataset Creation" tab after double-clicking `App.bat` or running `python app.py`, you can slice audio files to appropriate lengths and then automatically transcribe them. Or double-click `Dataset.bat` to open just that tab.
- After following the instructions, you can proceed to train on the "Training" tab below.

#### Training WebUI

- Follow the instructions from the "Training" tab in the WebUI opened by double-clicking `App.bat` or running `python app.py`. Or double-click `Train.bat` to open just that tab.

### Style Generation

- By default, in addition to the default style "Neutral", styles are generated according to the folder structure of the training folder.
- This is for those who want to manually create styles by other methods.
- You can generate styles using audio files from the "Style Creation" tab in the WebUI opened by double-clicking `App.bat` or running `python app.py`. Or double-click `StyleVectors.bat` to open just that tab.
- It's independent of training, so you can do it while training is in progress or redo it multiple times after training is complete (preprocessing must be finished).

### API Server

Running `python server_fastapi.py` in the configured environment will start the API server.
Check the API specification at `/docs` after startup.

- Input text length is limited to 100 characters by default. This can be changed with `server.limit` in `config.yml`.
- By default, CORS is enabled for all domains. Please change the `server.origins` value in `config.yml` to limit to trusted domains as much as possible (you can disable CORS by removing the key).

The API server for the speech synthesis editor is started with `python server_editor.py`. However, it's not fully organized yet. Currently, only the minimal necessary APIs from the [editor repository](https://github.com/litagin02/Style-Bert-VITS2-Editor) are implemented.

For web deployment of the speech synthesis editor, refer to [this Dockerfile](Dockerfile.deploy).

### Model Merging

You can mix two models at four points: "voice quality," "pitch," "emotional expression," and "tempo" to create a new model, or perform operations like "adding the difference between two models to another model."
From the "Merge" tab in the WebUI opened by double-clicking `App.bat` or running `python app.py`, you can select two models to merge. Or double-click `Merge.bat` to open just that tab.

### ONNX Conversion

You can convert trained safetensors files to ONNX format from the "ONNX Conversion" tab or `ConvertONNX.bat`. This is useful when ONNX format files are needed for external libraries. For example, [Aivis Project](https://aivis-project.com/) can create Aivis Speech models using [AIVM Generator](https://aivm-generator.aivis-project.com/) from safetensors and ONNX files.

### Naturalness Evaluation

We provide a script using [SpeechMOS](https://github.com/tarepan/SpeechMOS) as "one" indicator of which training step is best:
```bash
python speech_mos.py -m <model_name>
```
Naturalness evaluation per step is displayed, and results are saved to `mos_{model_name}.csv` and `mos_{model_name}.png` in the `mos_results` folder. If you want to change the text to be read, modify the file accordingly. This is ultimately a criterion that doesn't consider accent, emotional expression, or inflection at all, so it's just one guideline. I think it's best to actually synthesize and select by listening.

## Relationship with Bert-VITS2

This is basically just a slightly modified version of Bert-VITS2's model structure. Both the [older pretrained model](https://huggingface.co/litagin/Style-Bert-VITS2-1.0-base) and the [JP-Extra pretrained model](https://huggingface.co/litagin/Style-Bert-VITS2-2.0-base-JP-Extra) are essentially the same as Bert-VITS2 v2.1 or JP-Extra (with unnecessary weights removed and converted to safetensors).

Specifically, the following points differ:

- Easy to use even for people unfamiliar with Python or Git, like [EasyBertVits2](https://github.com/Zuntan03/EasyBertVits2).
- Changed the emotion embedding model (to 256-dimensional [wespeaker-voxceleb-resnet34-LM](https://huggingface.co/pyannote/wespeaker-voxceleb-resnet34-LM); more for speaker identification than emotion embedding)
- Removed vector quantization from emotion embeddings and made them simple fully connected layers.
- By creating a style vector file `style_vectors.npy`, you can generate speech while continuously specifying the strength of the effect using that style.
- Created various WebUIs
- Added support for bf16 training
- Added safetensors format support; uses safetensors by default
- Other minor bug fixes and refactoring


## References
In addition to the original reference (written below), I used the following repositories:
- [Bert-VITS2](https://github.com/fishaudio/Bert-VITS2)
- [EasyBertVits2](https://github.com/Zuntan03/EasyBertVits2)

[The pretrained model](https://huggingface.co/litagin/Style-Bert-VITS2-1.0-base) and [JP-Extra version](https://huggingface.co/litagin/Style-Bert-VITS2-2.0-base-JP-Extra) is essentially taken from [the original base model of Bert-VITS2 v2.1](https://huggingface.co/Garydesu/bert-vits2_base_model-2.1) and [JP-Extra pretrained model of Bert-VITS2](https://huggingface.co/Stardust-minus/Bert-VITS2-Japanese-Extra), so all the credits go to the original author ([Fish Audio](https://github.com/fishaudio)):


In addition, [text/user_dict/](text/user_dict) module is based on the following repositories:
- [voicevox_engine](https://github.com/VOICEVOX/voicevox_engine)
and the license of this module is LGPL v3.

## LICENSE

This repository is licensed under the GNU Affero General Public License v3.0, the same as the original Bert-VITS2 repository. For more details, see [LICENSE](LICENSE).

In addition, [text/user_dict/](text/user_dict) module is licensed under the GNU Lesser General Public License v3.0, inherited from the original VOICEVOX engine repository. For more details, see [LGPL_LICENSE](LGPL_LICENSE).



Below is the original README.md.
---

<div align="center">

<img alt="LOGO" src="https://cdn.jsdelivr.net/gh/fishaudio/fish-diffusion@main/images/logo_512x512.png" width="256" height="256" />

# Bert-VITS2

VITS2 Backbone with multilingual bert

For quick guide, please refer to `webui_preprocess.py`.

简易教程请参见 `webui_preprocess.py`。

## 请注意，本项目核心思路来源于[anyvoiceai/MassTTS](https://github.com/anyvoiceai/MassTTS) 一个非常好的tts项目
## MassTTS的演示demo为[ai版峰哥锐评峰哥本人,并找回了在金三角失落的腰子](https://www.bilibili.com/video/BV1w24y1c7z9)

[//]: # (## 本项目与[PlayVoice/vits_chinese]&#40;https://github.com/PlayVoice/vits_chinese&#41; 没有任何关系)

[//]: # ()
[//]: # (本仓库来源于之前朋友分享了ai峰哥的视频，本人被其中的效果惊艳，在自己尝试MassTTS以后发现fs在音质方面与vits有一定差距，并且training的pipeline比vits更复杂，因此按照其思路将bert)

## 成熟的旅行者/开拓者/舰长/博士/sensei/猎魔人/喵喵露/V应当参阅代码自己学习如何训练。

### 严禁将此项目用于一切违反《中华人民共和国宪法》，《中华人民共和国刑法》，《中华人民共和国治安管理处罚法》和《中华人民共和国民法典》之用途。
### 严禁用于任何政治相关用途。
#### Video:https://www.bilibili.com/video/BV1hp4y1K78E
#### Demo:https://www.bilibili.com/video/BV1TF411k78w
#### QQ Group：815818430
## References
+ [anyvoiceai/MassTTS](https://github.com/anyvoiceai/MassTTS)
+ [jaywalnut310/vits](https://github.com/jaywalnut310/vits)
+ [p0p4k/vits2_pytorch](https://github.com/p0p4k/vits2_pytorch)
+ [svc-develop-team/so-vits-svc](https://github.com/svc-develop-team/so-vits-svc)
+ [PaddlePaddle/PaddleSpeech](https://github.com/PaddlePaddle/PaddleSpeech)
+ [emotional-vits](https://github.com/innnky/emotional-vits)
+ [fish-speech](https://github.com/fishaudio/fish-speech)
+ [Bert-VITS2-UI](https://github.com/jiangyuxiaoxiao/Bert-VITS2-UI)
## 感谢所有贡献者作出的努力
<a href="https://github.com/fishaudio/Bert-VITS2/graphs/contributors" target="_blank">
  <img src="https://contrib.rocks/image?repo=fishaudio/Bert-VITS2"/>
</a>

[//]: # (# 本项目所有代码引用均已写明，bert部分代码思路来源于[AI峰哥]&#40;https://www.bilibili.com/video/BV1w24y1c7z9&#41;，与[vits_chinese]&#40;https://github.com/PlayVoice/vits_chinese&#41;无任何关系。欢迎各位查阅代码。同时，我们也对该开发者的[碰瓷，乃至开盒开发者的行为]&#40;https://www.bilibili.com/read/cv27101514/&#41;表示强烈谴责。)
