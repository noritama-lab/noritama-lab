# Noritama-Lab

製造業の生産技術エンジニアが個人開発している開発ラボです。  
現在は ESP32-S3 ベースの産業向けI/Oプラットフォーム「esp32ioシリーズ」を中心に公開しています。  
An individual R&D lab run by a manufacturing/production engineering engineer.  
Currently centered around the "esp32io" series — an industrial-oriented I/O platform based on ESP32-S3.

Home Assistantでの家庭用途から、工場の24V機器を扱う産業用途まで、  
**「配線するだけで、好きなソフトから制御できるI/Oデバイス」**を目指しています。  
From home automation with Home Assistant to industrial 24V equipment —  
the goal is a **wire-it-and-control-it-from-anything I/O device**.

---

## 🗺️ プロジェクト構成 / Project Overview

このエコシステムは、大きく分けて「ハードウェア」「ファームウェア（2系統）」「Pythonクライアント（2系統）」の3層で構成されています。  
This ecosystem consists of three layers: hardware, firmware (two variants), and Python clients (two variants).

| レイヤー / Layer | HTTP版 / HTTP version | MQTT版 / MQTT version |
|---|---|---|
| ファームウェア / Firmware | [esp32io-firmware](https://github.com/noritama-lab/esp32io-firmware) | [esp32io-mqtt-firmware](https://github.com/noritama-lab/esp32io-mqtt-firmware) |
| Pythonクライアント / Python client | [esp32io](https://pypi.org/project/esp32io/) (PyPI) / [esp32io-api](https://github.com/noritama-lab/esp32io-api) (GitHub) | [esp32io-mqtt](https://pypi.org/project/esp32io-mqtt/) (PyPI) / [esp32io-mqtt-api](https://github.com/noritama-lab/esp32io-mqtt-api) (GitHub) |
| ハードウェア / Hardware | [esp32io-hw](https://github.com/noritama-lab/esp32io-hw)（共通 / shared） | 同左 / same |

> ハードウェア（基板）はHTTP版・MQTT版で共通です。用途に応じてファームウェアを選択してください。  
> The PCB is shared between the HTTP and MQTT versions. Choose the firmware that fits your use case.

---

## 🔀 どちらを選べばいいか / Which One Should You Use?

| こんな人におすすめ / Recommended for | 選ぶべきもの / Choose |
|---|---|
| Home Assistantで自動検出したい、非同期でイベント駆動したい / Want Home Assistant auto-discovery, event-driven updates | **MQTT版** (esp32io-mqtt-firmware + esp32io-mqtt) |
| シンプルなHTTPリクエストで叩きたい、ブローカーを立てたくない / Want simple HTTP requests, no broker required | **HTTP版** (esp32io-firmware + esp32io) |
| Excel VBA・curlなど軽量な環境から使いたい / Want to control from lightweight environments like Excel VBA or curl | どちらでも可（生JSON API） / Either (raw JSON API available) |
| 工場の24Vリレー・センサーを安全に接続したい / Want to safely connect 24V industrial relays/sensors | **esp32io-hw**（オムロンLYシリーズ相当を想定） / esp32io-hw (designed for Omron LY-series relays or equivalent) |

---

## 🏠 Home Assistant連携 / Home Assistant Integration

**MQTT版**は、Home AssistantのMQTT Discoveryに対応しています。  
デバイスの電源を入れて配線するだけで、YAMLの手動設定なしにDI/DO/ADC/PWMなどが個別のエンティティとして自動的に登録されます。  
The **MQTT version** supports Home Assistant's MQTT Discovery.  
Simply power on and wire the device — DI/DO/ADC/PWM channels are automatically registered as individual entities without any manual YAML configuration.

デバイスIDはデバイス固有の値のため、複数台を同一ネットワークに追加してもトピックが衝突せず、  
Home Assistant側で自動的に別デバイスとして認識されます（実機2台で確認済み）。  
Since the device ID is unique to each unit, adding multiple devices to the same network does not cause topic collisions —  
each is recognized as a separate device in Home Assistant (verified with two physical devices).

---

## 🚀 はじめに / Getting Started

1. まずはESP32-S3-DevKitC-1などの開発ボードに、用途に応じて [esp32io-firmware](https://github.com/noritama-lab/esp32io-firmware) または [esp32io-mqtt-firmware](https://github.com/noritama-lab/esp32io-mqtt-firmware) を書き込み
2. 3.3V〜5Vのロジックレベルで使う場合は、開発ボードだけでそのまま利用可能です（[esp32io-hw](https://github.com/noritama-lab/esp32io-hw) は不要）
3. 工場の24V機器など、絶縁・保護回路が必要な環境で使う場合は [esp32io-hw](https://github.com/noritama-lab/esp32io-hw) のハードウェアを追加で用意
4. Python から使う場合は `pip install esp32io` または `pip install esp32io-mqtt`
5. Node-RED からは標準のHTTPリクエストノード、またはMQTTノードでそのまま接続可能

**English**

1. Flash [esp32io-firmware](https://github.com/noritama-lab/esp32io-firmware) or [esp32io-mqtt-firmware](https://github.com/noritama-lab/esp32io-mqtt-firmware) onto an ESP32-S3 dev board (e.g. ESP32-S3-DevKitC-1), depending on your use case
2. If you're working at 3.3V–5V logic levels, the dev board alone is sufficient ([esp32io-hw](https://github.com/noritama-lab/esp32io-hw) is not required)
3. For industrial 24V equipment requiring isolation and protection circuitry, add the [esp32io-hw](https://github.com/noritama-lab/esp32io-hw) hardware
4. For Python, run `pip install esp32io` or `pip install esp32io-mqtt`
5. For Node-RED, connect directly using the standard HTTP request node or MQTT node

---

## 📖 詳しい開発の背景 / Development Story

このプロジェクトは、「シリアル通信でPythonから制御したい」という最初の小さな動機から始まりました。  
This project started from a small idea: controlling things from Python over a serial connection.

- **USB/HTTP版までの開発記録**（シリアル通信からWi-Fi対応までの過程）  
  👉 [【開発記録】ESP32‑S3 × Python で作るI/Oデバイス連載](https://qiita.com/Noritama-Lab/items/cae87dc4cd67fe438c82)  
  👉 [ESP32-S3 をあらゆるソフトから制御できる IO プラットフォーム](https://qiita.com/Noritama-Lab/items/044451701336c6c17af4)
- **MQTT対応版への発展**（Home Assistant連携詳細記事は準備中）  
  👉 [自作のESP32-S3ベースIoTデバイス「ESP32IO」をMQTT対応へアップデート](https://qiita.com/Noritama-Lab/items/c074b20176145cb8e963)
- **プロジェクト全体の現在地**（HTTP版/MQTT版どちらも含む最新の全体像）  
  👉 [【現在地】ESP32-S3 IO プラットフォーム「esp32io」でできること](リンク後で追加)

Development records for the USB/HTTP version, and the subsequent MQTT update, are documented on Qiita (Japanese, linked above). For the latest overview covering both versions, see the "current state" article linked above.

---

## ⚠️ ご利用にあたって / Before You Use This

本プロジェクトは個人開発によるものであり、認証・第三者検証を受けたものではありません。  
実運用（特に産業機器への接続）前には、必ずご自身の環境・負荷条件に対する検証を行ってください。  
詳細は各リポジトリの README・免責事項をご確認ください。

This is an individually developed, open-source project without third-party certification.  
Please validate the design against your own environment before production use, especially when connecting to industrial equipment.  
See each repository's README and disclaimer for details.

---

## 🧩 その他のプロジェクト / Other Projects

esp32ioシリーズ以外にも、いくつかの小規模なツール・ライブラリを公開しています。  
Besides the esp32io series, a few smaller tools and libraries are also published here.

- [pyside6-stylekit](https://github.com/noritama-lab/pyside6-stylekit) — PySide6向けの自作UIキット（テーマ・スタイル済みウィジェット集） / A self-made UI kit for PySide6 (themes and pre-styled widgets)

> 今後も新しいプロジェクトが追加される可能性があります。最新の一覧は [Repositories タブ](https://github.com/noritama-lab?tab=repositories) をご確認ください。  
> More projects may be added over time. See the [Repositories tab](https://github.com/noritama-lab?tab=repositories) for the latest list.

---

## 🔗 リンク集 / Links

- GitHub: [github.com/noritama-lab](https://github.com/noritama-lab)
- Qiita: [qiita.com/Noritama-Lab](https://qiita.com/Noritama-Lab)
- X (Twitter): [@noritamalab](https://twitter.com/noritamalab)
