# SOUP Record — TI ADS1299 Linux Kernel IIO Driver

**IEC 62304 §8 — Software of Unknown Provenance (SOUP)**

| Field | Value |
|---|---|
| **SOUP Item** | ti-ads1298 / ADS1299 support — Linux kernel IIO ADC driver |
| **Version** | Patch submitted 2026-06-30 ([lore.kernel.org](https://lore.kernel.org/linux-iio/20260630140311.1473031-2-shofiqtest@gmail.com/)) |
| **Maintainer** | IIO subsystem — Jonathan Cameron (kernel.org) |
| **Source** | [drivers/iio/adc/ti-ads1298.c](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/drivers/iio/adc/ti-ads1298.c) |
| **License** | GPL-2.0 |
| **Purpose in device** | Acquires 8-channel 24-bit biopotential (EEG/EMG/EOG) signals over SPI at up to 16 kSPS |
| **Safety class (IEC 62304)** | Class B |

---

## Functional Description

The driver exposes the ADS1299 EEG ADC to the Linux IIO subsystem.
It handles SPI communication, register configuration, DRDY interrupt-driven
data acquisition, and IIO triggered buffer output.

Key operations:
- Device initialisation: SDATAC command, ID register read, CONFIG3 (reference) setup
- Per-channel gain configuration via CHnSET registers (PGA: 1/2/4/6/8/12/24)
- Continuous acquisition via DRDY falling-edge interrupt → async SPI → IIO push
- Single-shot acquisition for direct IIO read

---

## Known Anomalies and Limitations

| ID | Description | Severity | Mitigation |
|---|---|---|---|
| A-01 | Driver under upstream review — API may change before merge | Low | Pin kernel version; re-validate on kernel upgrade |
| A-02 | No on-chip lead-off detection exposed to userspace | Low | Implement lead-off monitoring at application layer |
| A-03 | Daisy-chain mode (multiple ADS1299) not supported | Medium | Use single-device configuration only |
| A-04 | GPIO START pin control not implemented — uses SPI command | Negligible | SPI START/STOP commands are functionally equivalent |

---

## Risk Classification (ISO 14971:2019)

| Hazard | Probability | Severity | Risk | Control |
|---|---|---|---|---|
| Incorrect EEG data due to SPI error | Low | High | Medium | SPI bus integrity check; data plausibility check at application layer |
| Missing DRDY interrupt (IRQ loss) | Very Low | Medium | Low | Watchdog timeout at application layer |
| Wrong channel gain applied | Low | High | Medium | Read-back CHnSET register after write; verify at init |
| Driver crash corrupts acquisition | Very Low | High | Medium | Linux kernel memory protection; process isolation |

---

## Verification Requirements (IEC 62304 §8.1.3)

- [ ] Verify SPI communication at target hardware clock frequency
- [ ] Validate 24-bit sample integrity against known reference signal
- [ ] Confirm DRDY interrupt latency meets real-time sampling requirements
- [ ] Test channel gain settings with known input voltage
- [ ] Verify triggered buffer output to userspace application
- [ ] Regression test on kernel LTS upgrade

---

## Change Control

| Date | Kernel version | Change | Author |
|---|---|---|---|
| 2026-06-30 | 6.x-rc | Initial SOUP record — patch under review | Md Shofiqul Islam |
