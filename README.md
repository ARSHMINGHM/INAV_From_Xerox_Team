# INAV From Xerox Team

🛰️ Backup & Configuration Archive for INAV-Based Multirotor Projects

This repository contains **blackbox logs**, **INAV configuration diffs**, **tuning screenshots**, and **historical backups** from the drone tuning and crash recovery processes by the Xerox Team. The purpose is to track, analyze, and maintain flight performance data and critical firmware settings for multiple configurations and revisions.

---

## 📁 Repository Structure
```
INAV_From_Xerox_Team/
│
├── Backups/ # INAV config backups + tuning screenshots
│ ├── 2025.04.29 (crash)/ # Logs from failed flight (crash case)
│ ├── 2025.05.21/ # Latest configuration snapshot
│ └── PreviousTeamBefore2025/ # Legacy setup from previous team
│
└── Blackboxes/ # Diff dumps of INAV CLI config (full logs)
├── 2025.05.18(AfterCrashFix)/ # Post-crash recovered & tuned config
└── 2025.05.28(AltHold)/ # Alt-hold mode focused tuning
```
---

## 🧰 Contents Overview

### 🔧 Backups/
- **`.txt` Files:** Full INAV CLI dumps from flight controller (v8.0.1)
- **`.png` Screenshots:**
  - *Tuning settings* (navigation, braking, PID, filters, failsafe)
  - *PID controller values*
  - *Receiver channel mappings*
  - *Failsafe settings*
  - *ESC/motor output configuration*
  - *Sensor configuration (e.g., ICM42605)*
- **Purpose:** Visual documentation of settings + crash analysis baseline

### 📦 Blackboxes/
- **`diff all` format:** Captures entire INAV configuration, including:
  - Feature flags (e.g., PWM_OUTPUT_ENABLE, OSD off)
  - Blackbox logging modules (e.g., NAV_POS, ATTI, RC_DATA)
  - Serial port settings and receiver mappings
  - Mixer profiles (motor direction, throttle response)
  - Control profiles: PID + filter tuning
  - Battery settings, failsafe behavior
- **Comparison between versions:**
  - *Pre-crash config* vs *Post-crash fix* (April → May)
  - *AltHold-specific config* tuned for hover performance

---

## 🧪 Tuning Summary

### Control Profiles (Example from `2025.05.28(AltHold)`)
| Axis  | P | I | D | FF |
|-------|---|---|---|----|
| Roll  | 45| 21| 20| 60 |
| Pitch | 50| 30| 25| 60 |
| Yaw   | 40| 35| 11| 60 |

### Gyro Filters
- LPF cutoff: 46 Hz  
- Dynamic Gyro Notch: Min 200 Hz → Max 500 Hz  
- Matrix Filter: Enabled (3D), Q = 250  

### Navigation
- AltHold Climb Rate: `200 cm/s`  
- Max Speed: `1000 cm/s`  
- Bank Angle Limit: `30°`

---

## 🛠 Hardware Notes

### Flight Controller
- `SPEEDYBEEF405AIO` and `TMOTORF7V2` (based on config versions)

### Sensors
- Accelerometer: `ICM42605` / `MPU6000`
- Barometer: `BMP280` (older config)
- No Magnetometer / GPS / Optical flow

### Receiver
- Protocol: `SBUS`
- Channel Map: `AETR`
- Failsafe: Land (1100 µs throttle for 2s)

---

## 🚩 Crashes & Recovery

### 🚫 April 29 Crash
- Files: `INAV_8.0.1_cli_20250429_*`
- Cause: Unstable PID or aggressive filter config
- Fix: Adjusted gyro LPF, blackbox logs changed, PID tuned

### ✅ May 18 Recovery
- New profile after crash with relaxed filters
- Lowered aggressiveness, added braking boost control

---

## ✅ Recommendations

- Use **blackbox logs** for debugging altitude hold and vibration issues.
- Refer to **Backups/2025.05.21** for the latest stable configuration.
- Tune around `d_boost_min`, `TPA`, and `yaw_rate` for aggressive flight styles.
- AltHold performance optimized in `2025.05.28(AltHold)`.

---

## 👥 Attribution

Maintained by the **Xerox Drone Team**  
INAV Firmware Version: `v8.0.1`  
Compiler: `GCC-13.2.1`

---

## 📄 License

This repository is for internal use and archival purposes. No specific license is applied unless stated otherwise.

