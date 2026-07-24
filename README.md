# Noritama-Lab

製造業の生産技術エンジニアが個人開発している、ESP32-S3ベースの産業向けI/Oプラットフォームです。  
An industrial-oriented I/O platform based on ESP32-S3, individually developed by a manufacturing/production engineering engineer.

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
| Pythonクライアント / Python client | [esp32io](https://pypi.org/project/esp32io/) (PyPI) | [esp32io-mqtt](https://pypi.org/project/esp32io-mqtt/) (PyPI) |
| ハードウェア / Hardware | [esp32io-hw](https://github.com/noritama-lab/esp32io-hw)（共通 / shared） | 同上 / same |

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

## 🚀 はじめに / Getting Started

1. まずは [esp32io-hw](https://github.com/noritama-lab/esp32io-hw) でハードウェアを用意（KiCad回路図・3Dプリント筐体データを公開）
2. 用途に応じて [esp32io-firmware](https://github.com/noritama-lab/esp32io-firmware) または [esp32io-mqtt-firmware](https://github.com/noritama-lab/esp32io-mqtt-firmware) を書き込み
3. Python から使う場合は `pip install esp32io` または `pip install esp32io-mqtt`
4. Node-RED からは標準のHTTPリクエストノード、またはMQTTノードでそのまま接続可能

---

## 📖 詳しい開発の背景 / Development Story

このプロジェクトは、「シリアル通信でPythonから制御したい」という最初の小さな動機から、  
HTTP版 → MQTT版 → Home Assistant対応 → Pythonクライアント → 産業向けハードウェア設計へと、  
実際に使いながら課題を解決する形で発展してきました。  

開発の経緯や技術的な詳細は、Qiitaでまとめています。  
The development story — from a simple serial-JSON idea to a full industrial I/O platform — is documented on Qiita (Japanese).

👉 [【まとめ記事】ESP32‑S3 × Python で作るI/Oデバイス連載](https://qiita.com/Noritama-Lab/items/cae87dc4cd67fe438c82)  
👉 [【完成】ESP32-S3 をあらゆるソフトから制御できる IO プラットフォーム](https://qiita.com/Noritama-Lab/items/044451701336c6c17af4)

---

## ⚠️ ご利用にあたって / Before You Use This

本プロジェクトは個人開発によるものであり、認証・第三者検証を受けたものではありません。  
実運用（特に産業機器への接続）前には、必ずご自身の環境・負荷条件に対する検証を行ってください。  
詳細は各リポジトリの README・免責事項をご確認ください。

This is an individually developed, open-source project without third-party certification.  
Please validate the design against your own environment before production use, especially when connecting to industrial equipment.  
See each repository's README and disclaimer for details.

---

## 🔗 リンク集 / Links

- GitHub: [github.com/noritama-lab](https://github.com/noritama-lab)
- Qiita: [qiita.com/Noritama-Lab](https://qiita.com/Noritama-Lab)
- X (Twitter): [@noritamalab](https://twitter.com/noritamalab)
