---
title: "TiRex on the Edge"
date: 2026-02-10T13:00:00+02:00
tags: ["Timeseries", "Benchmarking"]
cover:
  image: "img/thumbnail-edge.jpeg" # Needs to be inside your 'static' folder (e.g., static/img/my-preview-image.jpg)
  alt: "Generated image outlining different edge devices that were used for benchmarking."
  caption: ""
plotly: true
---

Time series are everywhere, shaping our everyday lives -- both professionally and privately. That's why time series models need to run quickly and reliably on many end devices, delivering predictions and classifications. But not every foundation model for time series is edge-capable. In our Edge Lab, we analyze the models, deploy them on various devices, and measure their performance and speed. After all, the industrial reality is PLCs or less powerful devices, and our goal is to find out how well foundation models perform on existing hardware.


{{< summary >}}
- [TiRex](https://arxiv.org/abs/2505.23719) is faster than Chronos-2 in inference and requires less energy. The forecast quality is only slightly worse. 
- TiRex is the best model when considering prediction quality (CRPS) and the ratio between latency and energy consumption. This makes TiRex ideal for industrial applications.
{{< /summary >}}

## Experiments

### Setup
We compare the performance of TiRex with all other models on **CPU**, considering that hardware acceleartors are rarely available on edge. We further test with the following settings:

```json
batch size:           1 (one series at a time)
prediction length:   32 steps
context size:      2048 steps
```

### Devices

| Device | Processor | RAM | Tested on |
|---|---|---:|---|
| Beckhoff C6015 | Intel Atom(R) x6416RE @ 1.70 GHz (4 cores) | 8 GB | CPU |
| KEBA Industrial PC | Intel(R) Core(TM) i7-6600U CPU @ 2.60GHz (dual core) | 16 GB | CPU |
| Bosch Rexroth ctrlX COREplus X3 | Zync Ultrascale+, 64-bit, 4 × ARM A53 | 2 GB | CPU |
| Raspberry Pi 5 | Arm Cortex-A76 @ 2.4GHz, 64-bit (4 cores) | 16 GB | CPU |
| NVIDIA Jetson Orin Nano Super | Arm Cortex-A78AE v8.2 64-bit (6 cores) | 8 GB | CPU |
| AMD Kria KR260 | Zynq™ UltraScale+™ MPSoC EV (XCK26) | 4 GB | CPU |

**Important**: This list is an initial selection and can be expanded as needed. Please contact us at contact@nx-ai.com if you would like to have your hardware tested as well.

## Results

Note that while the RAM range from 2 GB to 16 GB is striking, TiRex runs smoothly on all devices. Below you can find out how it fares against its competitors.

Across all edge devices combined, TiRex sits on the Pareto front for both inference latency and energy consumption, trading a small amount of forecast quality (CRPS) for a clear speed and efficiency advantage over the competition.

### Prediction Quality vs. Latency
{{< plotly json="plots/edge-comparison-latency.json" height="570px">}}

### Prediction Quality vs. Energy Consumption
{{< plotly json="plots/edge-comparison-energy.json" height="570px">}}

{{< plotly json="plots/bars-raspberry-pi.json" height="500px" width="900px">}}
{{< plotly json="plots/bars-keba-plc.json" height="500px" width="900px">}}
{{< plotly json="plots/bars-beckhoff-c6015.json" height="500px" width="900px">}}

{{< summary title="Take Away" >}}
- TiRex is faster than Chronos-2 in inference and requires less energy. The forecast quality is only slightly worse.
- TiRex is the best model when considering prediction quality (CRPS) and the ratio between latency and energy consumption. This makes TiRex ideal for industrial applications.
{{< /summary >}}