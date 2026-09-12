# Sumitsuke

**サイト → [sumitsuke.jp](https://sumitsuke.jp/)**（受託開発・検証の案内と、実験の記録 Lab）

AI生成コード・外注コードの検証・監査（再現 → 原因 → 修正 → 検証ログ）と、
Rust/Tauri による Windows local-first デスクトップアプリ開発をしています。

Verification & audit of AI-generated code (reproduce → root-cause → fix → verification logs), and Windows local-first desktop apps in Rust/Tauri.

**ご相談はこちら → [sumitsuke.jp/works/contact/](https://sumitsuke.jp/works/contact/)**（テキスト完結・通話なし）

---

## 何を依頼できるか

- **AI生成・外注コードの検証・監査** — 症状の再現を試み、原因（または原因候補と除外できた原因）を特定し、修正し、実行ログ・テストで再確認するまでを一続きで行います。AIの回答だけで判断せず、実際の実行結果を基準にします。
- **不具合の根本デバッグ** — 「計算される値 ≠ DBに保存される値 ≠ 読み取り時の値」のような多層にまたがるバグの往復トレースと根治。
- **Windowsデスクトップアプリ開発** — Rust/Tauri + React/TypeScript。データを外部に送らない local-first 設計。

## 自社開発: AXIOM（クローズドβ）

測定系の Windows デスクトップアプリを、設計から配布構成までソロで開発しています。現在**クローズドβ**（v0.2.0-beta.2）。 → [getaxiom.dev](https://getaxiom.dev/)

- Rust 約77,000行 + React/TypeScript 約40,000行（本体のみ）
- テスト**約3,200件を release 実行で全PASS**（2026-06-23、実行ログで確認）
- SQLite + アプリ層 AES-256-GCM のローカル暗号化データ層／Rust⇄TS を 102 IPC・自動生成型バインディング（ts-rs）で接続
- 外部通信は許可リスト制で、**許可外の送信経路の追加をCIがビルド失敗で止める**（宣言をコードで強制）

AIコーディングを実装に多用しつつ、AIの出力を鵜呑みにしない検証規律を敷いています。実際に検出・修正した AI 起因の欠陥（いずれも commit で検証可能）:

- 存在しない学術引用の混入を検出し、測定挙動を変えずに除去
- 「ハッシュ列の書き換えと再ハッシュが別トランザクション」という多層整合性バグを、1トランザクションへのアトミック化で根治
- 失敗を握り潰すフォールバックの増加・型ずれ・送信経路の無断追加を、**AIの失敗モードを狙い撃つ自作CIゲート**（anti-dummy-scan / outbound-network-guard / bindings-drift-gate）で再発防止

※ クローズドβのため、利用者数・本番運用スケールは主張しません。

## 公開している検証成果物

再現可能な実測・監査の公開リポジトリ（ピン留め参照）:

- [llm-audit-nondeterminism](https://github.com/sumitsuke/llm-audit-nondeterminism) — 同じコードをローカルLLMにN回監査させたときの指摘の揺れ（反復非決定性）と多数決の落とし穴を実測する再現キット
- [free-tier-vectordb-bench](https://github.com/sumitsuke/free-tier-vectordb-bench) — 無料枠だけで4つのベクトルDBへ同一RAGを流し、品質・レイテンシ・律速ユニットを再現可能に実測するハーネス
- [zenn-content](https://github.com/sumitsuke/zenn-content) — Zenn掲載の実測記事の原稿・図（GitHub連携）

数値は実測のみ。検証していない数字は書かない方針です。

## 対応技術

Rust / Tauri ・ React / TypeScript ・ SQLite ・ Windows local-first（ローカル保存・外部送信最小）

## 診断レポート見本

不具合診断の納品形式（再現確認・原因・影響範囲・修正方針を2〜4ページに整理）の**見本があります**。自社開発アプリを題材にしたサンプルで、顧客案件の実績ではありません。ご相談時にご覧いただけます。

## 相談先

**[sumitsuke.jp/works/contact/](https://sumitsuke.jp/works/contact/)** — 診断・修正・開発のご相談はこちらから（テキスト完結・通話なし）

