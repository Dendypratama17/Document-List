# 📱 Appium Setup Guide (Python + Pytest - macOS)

## 📌 Prerequisites

Sebelum install Appium, pastikan di MacBook kamu sudah ada:

- Homebrew
- Node.js
- Python 3
- Android Studio
- JDK
- Xcode (untuk iOS automation)

### 🔍 Cek Instalasi
```bash
brew -v
node -v
npm -v
python3 --version
java -version
```

---

## 🛠️ 1. Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew -v
```

---

## 🛠️ 2. Install Node.js

```bash
brew install node
node -v
npm -v
```

---

## 🛠️ 3. Install Python & Pytest

```bash
brew install python
python3 --version
pip3 --version
```

Install dependencies:

```bash
pip3 install pytest Appium-Python-Client
pip3 install pytest-html pytest-xdist
```

---

## 🛠️ 4. Install Java

```bash
brew install openjdk
echo 'export PATH="/opt/homebrew/opt/openjdk/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
java -version
```

---

## 🛠️ 5. Install Android Studio

Install dan pastikan komponen berikut:
- Android SDK
- Platform Tools
- Emulator
- Build Tools

### Setup Environment
```bash
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin

source ~/.zshrc
```

### Cek ADB
```bash
adb version
adb devices
```

---

## 🛠️ 6. Install Appium 2

```bash
npm install -g appium
appium -v
```

Install driver:

```bash
appium driver install uiautomator2
# Optional iOS
appium driver install xcuitest
```

---

## 🛠️ 7. Install Appium Doctor

```bash
npm install -g appium-doctor
appium-doctor --android
# Optional
appium-doctor --ios
```

---

## ▶️ 8. Jalankan Appium Server

```bash
appium
```

---

## 📁 9. Struktur Project

```
mobile-automation/
│
├── tests/
│   └── test_login.py
│
├── conftest.py
├── requirements.txt
└── pytest.ini
```

---

## ⚙️ 10. conftest.py

```python
from appium import webdriver
from appium.options.android import UiAutomator2Options
import pytest

@pytest.fixture()
def driver():
    options = UiAutomator2Options()
    options.platform_name = "Android"
    options.device_name = "Android Emulator"
    options.automation_name = "UiAutomator2"
    options.app = "/Users/yourname/apps/app-debug.apk"

    driver = webdriver.Remote(
        "http://127.0.0.1:4723",
        options=options
    )

    yield driver
    driver.quit()
```

---

## 🧪 11. Sample Test

```python
def test_open_app(driver):
    assert driver.is_app_installed("com.example.app")
```

---

## ▶️ 12. Run Test

```bash
pytest -v
pytest -v --html=report.html
```

---

## 🤖 13. Emulator Setup

```bash
adb devices
```

Output:
```
emulator-5554 device
```

---

## 🍏 14. iOS Setup (Optional)

```bash
xcode-select --install
sudo xcodebuild -license accept
appium driver install xcuitest
```

---

## ✅ Summary

- Gunakan Appium untuk cross-platform mobile testing
- Gunakan Pytest untuk test runner
- Pastikan environment sudah valid dengan appium-doctor
- Gunakan emulator atau real device

---
