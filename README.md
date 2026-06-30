# IEC 62304 Compliance Documents for Embedded OSS Drivers

IEC 62304-aligned documentation for upstream open source embedded drivers.
Every document is based on a **real merged driver** — not a hypothetical.

If your medical device runs **Zephyr RTOS** or the **Linux kernel** and uses
any of these drivers, you can use these documents as a starting point for your
own IEC 62304 software lifecycle documentation.

> **Disclaimer:** These are reference documents and templates.
> They must be reviewed and adapted by a qualified engineer for your specific
> product and regulatory jurisdiction. They are not pre-certified audit artefacts.

---

## Covered Drivers

| Driver | Platform | Documents |
|---|---|---|
| **MAX30102** SpO₂ / Heart Rate | Zephyr RTOS ([PR #108697](https://github.com/zephyrproject-rtos/zephyr/pull/108697) ✅ merged) | SRS · SDS · SOUP · FMEA |
| **ADS1299** EEG / Biopotential ADC | Linux kernel IIO ([patch submitted](https://lore.kernel.org/linux-iio/20260630140311.1473031-2-shofiqtest@gmail.com/)) | SOUP · FMEA |

---

## Documents

### MAX30102 — Zephyr RTOS SpO₂ / Heart Rate Sensor Driver

| Document | IEC 62304 Clause | Description |
|---|---|---|
| [Software Requirements Specification](SRS_MAX30102_Driver.md) | §5.2 | 12 shall-statements covering functional, performance, interface and safety requirements |
| [Software Design Specification](SDS_MAX30102_Driver.md) | §5.4 | Architecture, component design, interfaces, timing, concurrency model |
| [SOUP Record](SOUP_Record_MAX30102_Driver.md) | §8 | SOUP identification, known anomalies, risk classification, verification |
| [FMEA](FMEA_MAX30102_Driver.md) | ISO 14971:2019 | 8 failure modes — severity, probability, risk level, mitigations |

### ADS1299 — Linux Kernel IIO EEG / Biopotential ADC Driver

| Document | IEC 62304 Clause | Description |
|---|---|---|
| [SOUP Record](SOUP_Record_ADS1299_Driver.md) | §8 | SOUP identification, known anomalies, risk classification, verification |
| [FMEA](FMEA_ADS1299_Driver.md) | ISO 14971:2019 | Failure modes for 24-bit EEG acquisition — signal integrity, saturation, SPI errors |

---

## Who is this for?

- Medical device teams using **Zephyr RTOS** with Nordic nRF or similar SoCs
- Teams building **Linux-based** patient monitoring or diagnostics equipment
- Startups needing a **head start** on IEC 62304 documentation for OSS components
- Engineers preparing for **FDA 510(k)** or **CE marking** submissions using these drivers

---

## Author

These documents were written by the same engineer who wrote the drivers:

- **MAX30102 Zephyr driver** — merged upstream ([PR #108697](https://github.com/zephyrproject-rtos/zephyr/pull/108697))
- **ADS1299 Linux IIO driver** — first upstream EEG ADC driver ([lore.kernel.org](https://lore.kernel.org/linux-iio/20260630140311.1473031-2-shofiqtest@gmail.com/))
- **MAX86150 Linux IIO driver** — ECG + PPG ([lore.kernel.org](https://lore.kernel.org/linux-iio/20260623140113.12574-1-shofiqtest@gmail.com/))

Contact: [shofiqtest@gmail.com](mailto:shofiqtest@gmail.com)
