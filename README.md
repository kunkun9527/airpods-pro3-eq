# AirPods Pro 3 PEQ（约 60% 音量，按 5128 测量拟合）

把 AirPods Pro 3 的频响拟合到几条常见目标曲线（LMG 0.6、JM-1 −10 dB tilt、Harman 2025 MoA、IEF Preference 2025、SoundGuys）上得到的参数式均衡器（PEQ）。每条目标都有 6 kHz 和 12 kHz 两个拟合上限版本。

> **注意**：测量曲线是多家 B&K 5128 数据综合出来的 **60% 音量估计**，不是对你这副耳机的实测。耳机固件版本、耳塞套、佩戴位置、降噪状态和音量都会改变响应，请把它当作起点，而不是标准答案。

## 文件

| 路径 | 内容 |
|---|---|
| `presets/*.txt` | PEQ 参数，Equalizer APO 格式（`Preamp` + `Filter N: ON ...`） |
| `plots/fit_*.png` | 每条目标的拟合结果：估计测量、目标曲线、拟合后响应，以及 EQ 曲线 |

文件名格式为 `<目标>_<上限>.txt`，例如 `LMG06_12k.txt` 表示 LMG 0.6 目标、拟合到 12 kHz。

## 使用

1. 把 `presets/` 里的 `.txt` 导入支持 Equalizer APO 格式的均衡器（Windows 上的 Equalizer APO，或 Peace 等）。Android 上的 App 不一定都支持这个格式，导入前先确认。
2. 把 `Preamp` 的值一起设上，这是为了给提升的频段留余量，避免削波。
3. 从 12 kHz 版本开始听。6 kHz 版本在 6 kHz 以上完全不修正，更保守。
4. 比较不同预设时，**音量保持不变**。这些预设已经做过等响度对齐，但对齐只是按粉红噪声估算，听感差 ±0.5 dB 是正常的。

## 目标曲线

| 文件 | 目标 | 说明 |
|---|---|---|
| `LMG06_*` | LMG 0.6 | LTT Labs 的 B&K 5128 目标，偏向"偏好"取向 |
| `JM1-10dB_*` | JM-1 −10 dB tilt | JM-1 5128 目标，加了 −1 dB/oct 的倾斜（比 5128 JM-1 更暗） |
| `Harman25_*` | Harman 2025 MoA | Harman 2025 年的平均目标 |
| `IEF25_*` | IEF Preference 2025 | 基于 JM-1 加低频提升、高频降低的偏好版 |
| `SoundGuys_*` | SoundGuys | SoundGuys 的 5128 目标 |

目标曲线的数据版权归各自的发布方所有。这里只给出拟合后的 PEQ 参数，不包含原始目标数据。

## 数据来源（原始数据不在本仓库中）

以下是拟合所用数据的来源网站。具体条目的深层链接没有逐一记录，请在站内搜索 `AirPods Pro 3` 或 `5128`。

| 来源 | 网址 | 用途 |
|---|---|---|
| earphonesarchive | https://earphonesarchive.squig.link/ | AirPods Pro 3 的 B&K 5128 测量（iPhone，vol-4，ANC 开/关、通透），以及部分目标 |
| Hangout / Crinacle 5128 | https://graph.hangout.audio/iem/5128 | AirPods Pro 3 的 5128 测量（macOS、Windows、多次佩戴），以及 LMG 0.6、JM-1、Harman 2025、IEF 2025、SoundGuys 目标 |
| headphones.com GraphWorks | https://headphones.com/ （产品 slug `airpods-pro-3`） | 16 个音量档的 5128 测量（测量 ID `cmqtqbexe000004jv2mqogkh0`） |
| squig.link | https://squig.link/ | 711 耳机耦合器测量，不是 5128，只用于估算 60% 音量的变化量 |

拉取时间：2026-11 月。测量站点的数据随时可能更新，建议以当时页面为准。

## 拟合方法

- 测量基线：多家 B&K 5128 测量在 200 Hz–2 kHz 对齐后综合，再用其他来源的音量变化估算到约 60% 音量。
- 拟合目标：目标曲线 − 测量曲线，只拟合 1/6 倍频程平滑后的误差。
- 滤波器：1 个低架 + 8 个峰值滤波器。上限以上的 EQ 保持为 0 dB。
- 增益惩罚：每 dB 增益 0.3 的平方惩罚，防止大正大负互相抵消。拟合后合并重复的滤波器（同频率、同 Q），再精修一次。
- 误差：拟合范围内各段 RMS 多数在 0.1–0.6 dB 之间，10–12 kHz 段最大约 0.6 dB（12 kHz 版本）。

## 没有包含的内容

- 原始测量数据（各站点的 CSV / 原始 JSON）
- 目标曲线的原始 CSV
- 带 MSEB（TempoTec V1 的低频 +2 dB、空气感 +2 dB 等）的版本
- V4A 的 DDC 文件（`.vdc`）

## 局限

- 只有一种测量条件（原装耳塞套、开降噪、约 60% 音量）。换耳塞套、关降噪或音量变化，响应都会改变。
- 60% 音量的测量曲线是**估算**，不是实测。
- 目标曲线本身有取舍（例如 LMG 0.6 的数值含义没有完全公开确认），选哪条取决于你的口味。
- 高于 10 kHz 的修正依据较弱，各家测量差异也大，建议用 6 kHz 版本或直接不修正。

## 许可

待定。
