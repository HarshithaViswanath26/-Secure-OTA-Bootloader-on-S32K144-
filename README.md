
---

## 🛠️ Development Plan & Milestones

### 🔹 Phase 1: Bootloader (Weeks 1–2)
- Configure S32K144 in standalone bootloader mode
- Flash partitioning for bootloader and main app
- UART (or CAN) peripheral setup
- Command parser: `START`, `SEND_CHUNK`, `VERIFY`, `REBOOT`

### 🔹 Phase 2: Firmware Encryption & Verification (Week 3)
- Implement AES-128 decryption (software/hardware)
- Add SHA-256 or CRC32 checksum validation
- Optional: RSA digital signature verification
- Error indication via LEDs or fallback routine

### 🔹 Phase 3: OTA Firmware Sender App (Week 4)
- Python-based tool:
  - Encrypt and chunk firmware binary
  - Send metadata and binary via UART
  - Track update status and feedback

### 🔹 Phase 4: Application with FreeRTOS (Week 5)
- Create 2–3 FreeRTOS tasks:
  - LED blinking
  - OTA update listener
  - Diagnostics and version output
- Support version identification on terminal

### 🔹 Phase 5: Fail-safe Mechanism (Week 6)
- Backup firmware slot (if space allows)
- Power-loss recovery with rollback to previous version
- Store state in EEPROM/Flash

---

## 🧪 Test Cases & Validation

| Test Case                  | Expected Outcome                         |
|---------------------------|------------------------------------------|
| Normal firmware upload     | Decrypts, writes, reboots to new version |
| Corrupt binary sent        | Shows error, doesn't boot new app        |
| Power loss during upload   | Rolls back to old working version        |
| Wrong signature            | Fails update, does not boot              |
| CAN instead of UART (opt.) | Works with CAN, demonstrates flexibility |

---

## 🧰 Tools Required

| Tool/Library            | Purpose                             |
|-------------------------|-------------------------------------|
| **S32 Design Studio**   | Build & flash S32K144 MCU           |
| **FreeRTOS**            | RTOS for application logic          |
| **OpenSSL/PyCrypto**    | Firmware encryption & signing       |
| **Python (PySerial)**   | OTA desktop tool communication      |
| **UART/USB/CAN dongle** | MCU communication interface         |
| **Oscilloscope (opt.)** | Timing/debugging for UART/CAN       |

---

## 📄 Summary

Developed a secure bootloader supporting AES-128 encrypted OTA firmware updates over UART with integrity checks and rollback. Integrated a FreeRTOS-based main application with multi-version firmware control. Built a Python OTA tool to automate secure firmware delivery and verified support for power-loss recovery and digital signature validation.

---

## 📸 Preview

![Architecture Diagram](docs/architecture.png)

---

## 📬 Contact

Feel free to reach out via [LinkedIn](#) or open an issue for suggestions or questions.
