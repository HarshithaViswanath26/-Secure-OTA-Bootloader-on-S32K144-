# -Secure-OTA-Bootloader-on-S32K144-

1. S32K144-SecureOTA/
│
├── bootloader/
│   ├── src/
│   ├── inc/
│   ├── linker.ld
│   └── .project
│
├── app/
│   ├── FreeRTOS/
│   ├── src/
│   ├── version.h
│   └── main.c
│
├── ota_tool/
│   ├── ota_sender.py
│   └── readme.md
│
├── docs/
│   ├── architecture.png
│   ├── test_log.md
│   └── user_manual.pdf
│
└── README.md


🛠️ 2. Development Plan & Milestones
🔹 Phase 1: Bootloader (Weeks 1–2)
- Configure S32K144 in standalone bootloader mode
- Flash partitioning (decide flash space for bootloader vs app)
- UART/CAN peripheral setup (start with UART for simplicity)
- Command parser for:
  START, SEND_CHUNK, VERIFY, REBOOT

🔹 Phase 2: Firmware Encryption & Verification (Week 3)
- Implement AES-128 decryption using software or hardware module
- Add SHA-256 or CRC32 hash validation
- Digital signature support (optional, can use a pre-generated RSA key for demo)
- If invalid – show LED error / fallback

🔹 Phase 3: OTA Firmware Sender App (Week 4)
- Develop a Python desktop tool:
- Select firmware binary
- Chunk it, encrypt it, send via UART
- Send version number / metadata

🔹 Phase 4: Application with FreeRTOS (Week 5)
- FreeRTOS with 2–3 tasks:
- LED Blink
- OTA Update Listener
- Diagnostic Info Print
- Make it version-aware (e.g., v1.0, v2.0… visible on terminal)

🔹 Phase 5: Fail-safe Mechanism (Week 6)
- Add a backup firmware slot (if flash allows)
- If OTA fails or power-loss → rollback to previous working app
- Store state in flash/eeprom

🧪 3. Test Cases & Validation

| Test Case                  | Expected Outcome                         |
| -------------------------- | ---------------------------------------- |
| Normal firmware upload     | Decrypts, writes, reboots to new version |
| Corrupt binary sent        | Shows error, doesn't boot new app        |
| Power loss during upload   | Boots old version (rollback works)       |
| Wrong signature            | Fails update, reverts                    |
| CAN instead of UART (opt.) | Works with CAN, shows flexibility        |

🧰 4. Tools Required

| Tool/Library            | Purpose                           |
| ----------------------- | --------------------------------- |
| **S32 Design Studio**   | For building and flashing S32K144 |
| **FreeRTOS**            | RTOS for main application         |
| **OpenSSL/PyCrypto**    | For AES encryption/signature      |
| **Python (PySerial)**   | For the OTA PC uploader tool      |
| **UART/USB/CAN dongle** | Interface with MCU                |
| **Oscilloscope (opt.)** | Debugging CAN/UART timing         |


Developed a secure bootloader supporting AES-128 encrypted OTA firmware updates over UART with integrity checks and rollback. Integrated FreeRTOS-based main application with multi-version firmware control. Created Python OTA tool and verified power-loss recovery and digital signature validation.

