# AirPods Pro 3 PEQ (≈60% volume, fitted to B&K 5128 measurements)

**English** | [中文](README.zh-CN.md)

Parametric EQ (PEQ) presets that fit the AirPods Pro 3 response to four target curves: JM-1 −10 dB tilt, Harman 2025 MoA, IEF Preference 2025 and SoundGuys. Each target has a 6 kHz and a 12 kHz fit-range version.

The measurement is an estimate of the response at about 60% volume, combined from several B&K 5128 measurements. It is not a measurement of a single unit.

## Fit results

Each plot shows the estimated measurement (black), the target (dashed grey), the response after EQ at 6 kHz (red) and 12 kHz (blue), and the EQ curves with the ideal correction (target − measurement).

### JM-1 −10 dB tilt
![JM-1 -10 dB tilt fit](plots/fit_JM1-10dB.png)

### Harman 2025 MoA
![Harman 2025 MoA fit](plots/fit_Harman25.png)

### IEF Preference 2025
![IEF Preference 2025 fit](plots/fit_IEF25.png)

### SoundGuys
![SoundGuys fit](plots/fit_SoundGuys.png)

## Files

| Path | Content |
|---|---|
| `presets/*.txt` | PEQ filters in Equalizer APO format (`Preamp` + `Filter N: ON ...`) |
| `plots/fit_*.png` | Fit result for each target |

Naming: `<target>_<range>.txt`, e.g. `Harman25_12k.txt` is the Harman 2025 MoA target fitted up to 12 kHz.

## Usage

1. Import a preset into an app that reads Equalizer APO format, such as Equalizer APO on Windows or Peace.
2. Set the `Preamp` value as well. It leaves headroom for the boosted bands.
3. The 12 kHz versions cover the full range of the fit. The 6 kHz versions leave everything above 6 kHz unchanged.
4. Keep the volume fixed when comparing presets. The presets are loudness-matched using pink noise, so perceived differences of about ±0.5 dB remain.

## Targets

| Preset prefix | Target | Notes |
|---|---|---|
| `JM1-10dB_*` | JM-1 −10 dB tilt | JM-1 5128 target with a −1 dB/octave tilt, darker than plain JM-1 |
| `Harman25_*` | Harman 2025 MoA | Harman 2025 average target |
| `IEF25_*` | IEF Preference 2025 | Preference version of JM-1 with more bass and less treble |
| `SoundGuys_*` | SoundGuys | SoundGuys 5128 target |

The target data belongs to its publishers. This repository contains only the fitted PEQ parameters.

## Data sources

Raw data is not included in this repository.

| Source | URL | Used for |
|---|---|---|
| earphonesarchive | https://earphonesarchive.squig.link/ | B&K 5128 measurements of AirPods Pro 3 (iPhone, vol-4, ANC on/off, transparency) and some targets |
| Hangout / Crinacle 5128 | https://graph.hangout.audio/iem/5128 | B&K 5128 measurements of AirPods Pro 3 (macOS, Windows, multiple seatings) and the JM-1, Harman 2025, IEF 2025 and SoundGuys targets |
| headphones.com GraphWorks | [headphones.com](https://headphones.com/) (product slug `airpods-pro-3`) | 16 volume-setting 5128 measurements (measurement ID `cmqtqbexe000004jv2mqogkh0`) |

Data retrieved in November 2026.

## Method

- **Measurement baseline:** 5128 measurements from the sources above are aligned at 200 Hz–2 kHz and averaged. The result is adjusted to about 60% volume using the volume changes observed in the sources.
- **Fit target:** target − measurement, fitted to the error smoothed at 1/6 octave.
- **Filters:** one low shelf and eight peaking filters. The EQ is 0 dB above the fit range.
- **Regularisation:** a squared penalty of 0.3 per dB of gain. After fitting, duplicate filters (same frequency and Q) are merged and the remaining filters are refitted once.
- **Error:** RMS error inside the fit range is mostly 0.1–0.6 dB. In the 12 kHz versions, the 10–12 kHz band reaches about 0.6 dB.

## Not included

- Raw measurement data and raw target CSVs
- The MSEB variant (TempoTec V1 bass +2 dB, air +2 dB)
- V4A DDC files (`.vdc`)

## Limitations

- One measurement condition: stock ear tips, ANC on, about 60% volume. Other tips, ANC off or other volume levels change the response.
- Each target reflects a particular choice of tuning.
- Above 10 kHz the sources disagree substantially, so the corrections there are the least reliable. The 6 kHz versions avoid that region.

## License

To be decided.
