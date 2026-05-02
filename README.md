# 🌐 Global Asset Delivery Network (CDN) Infrastructure

![Infrastructure Status](https://img.shields.io/badge/Infrastructure-Operational-brightgreen?style=flat-square)
![CDN Uptime](https://img.shields.io/badge/CDN_Uptime-99.99%25-blue?style=flat-square)
![Security](https://img.shields.io/badge/Security-Strict-critical?style=flat-square)
![Deployment](https://img.shields.io/badge/Deployment-Automated-success?style=flat-square)

---

## 📌 Table of Contents
- [日本語](#-日本語)
- [English](#-english)

---

## 🇯🇵 日本語

### 📌 目次
- [1. エグゼクティブ・サマリ](#1-エグゼクティブサマリ)
- [2. 主要機能とサービスレベル](#2-主要機能とサービスレベル)
- [3. インテグレーション・ガイドライン](#3-インテグレーションガイドライン)
- [4. ディレクトリ構造と分類学](#4-ディレクトリ構造と分類学)
- [5. アセット最適化仕様](#5-アセット最適化仕様)
- [6. キャッシュ無効化戦略](#6-キャッシュ無効化戦略)
- [7. セキュリティポリシー](#7-セキュリティポリシー)
- [8. 監視と可観測性](#8-監視と可観測性)
- [9. トラブルシューティング](#9-トラブルシューティング)

---

### 1. エグゼクティブ・サマリ

本リポジトリは、モダンWebアプリケーションおよび各種デジタルプロダクトにおいて使用される静的アセット（Static Assets）を、超低遅延（Ultra-Low Latency）で世界中に配信するためのCDNインフラストラクチャです。

GitHubをオリジンストレージとして採用し、jsDelivrのマルチCDNネットワーク（Cloudflare / Fastly / Bunny CDN等）を経由することで、エンタープライズレベルの信頼性とパフォーマンスを実現します。

---

### 2. 主要機能とサービスレベル

#### 🎯 基本原則

##### 1. 高可用性（High Availability）
- マルチCDNによる自動フェイルオーバー
- 障害時の即時ルーティング切替
- SLA: 99.99% Uptime

##### 2. 不変性（Immutability）
- Git commit hash または SemVer による完全固定
- キャッシュポイズニング防止

##### 3. パフォーマンス最適化
- Brotli / Gzip 圧縮
- HTTP/2 / HTTP/3 対応
- 長期キャッシュ戦略

##### 4. グローバルエッジ配信
- 世界中のエッジロケーションから配信
- 最短経路ルーティング

---

### 3. インテグレーション・ガイドライン

#### 3.1 CDN URL スキーム

```text
https://cdn.jsdelivr.net/gh/{username}/{repo}@{version}/{path}
```

#### 3.2 実装例（Next.js）

```ts
export const CDN_BASE_URL = "https://cdn.jsdelivr.net/gh/Username/Repo@main";
```

```tsx
<link rel="preconnect" href="https://cdn.jsdelivr.net" crossOrigin="anonymous" />
<link rel="stylesheet" href={`${CDN_BASE_URL}/styles/main.min.css`} />
```

---

#### 3.3 AIモデル配信

```ts
import { pipeline, env } from "@xenova/transformers";

env.localModelPath = "https://cdn.jsdelivr.net/gh/Username/Repo@main/assets/models/";

const classifier = await pipeline("sentiment-analysis", "custom-model");
```

---

### 4. ディレクトリ構造と分類学

```plaintext
/
├── assets/
│   ├── images/
│   │   ├── branding/
│   │   └── ui/
│   ├── models/
│   │   ├── onnx/
│   │   └── safetensors/
│   ├── scripts/
│   │   ├── core/
│   │   └── ai-workers/
│   ├── styles/
│   │   ├── tailwind/
│   │   └── design-systems/
│   └── typography/
│       ├── product-sans/
│       └── display/
├── docs/
├── .github/
└── README.md
```

---

### 5. アセット最適化仕様

#### 5.1 タイポグラフィ
- .woff2 のみ使用
- サブセット化必須

#### 5.2 画像
- WebP / AVIF 推奨
- SVG最適化

#### 5.3 AIモデル
- int8 / uint8 量子化
- 50MB以下（超える場合は分割）

#### 5.4 ネーミング規則

```text
[a-z0-9-]
```

---

### 6. キャッシュ無効化戦略

#### 推奨: Cache Busting
```
@v1.0.0 → @v1.0.1
```

#### 強制パージ

```bash
curl https://purge.jsdelivr.net/gh/Username/Repo@main/file.css
```

---

### 7. セキュリティポリシー

#### シークレット禁止ポリシー
- APIキー禁止
- パスワード禁止

#### CORS

```http
Access-Control-Allow-Origin: *
```

---

### 8. 監視と可観測性

#### 確認項目
- レイテンシ
- キャッシュヒット率

#### デバッグ

```http
x-cache: HIT / MISS
```

---

### 9. トラブルシューティング

#### 404 Not Found
- バージョン確認
- パス確認

#### 403 Forbidden
- サイズ制限確認（50MB）

#### 遅延
- 初回MISS確認
- 再アクセスでHIT確認

---

### 👨‍💻 メンテナー
Core Systems Engineering Team

---

### 📄 ライセンス
MIT License

---

## 🇬🇧 English

### 📌 Table of Contents
- [1. Executive Summary](#1-executive-summary)
- [2. Core Capabilities & SLAs](#2-core-capabilities--slas)
- [3. Integration Guidelines](#3-integration-guidelines)
- [4. Directory Architecture & Typology](#4-directory-architecture--typology)
- [5. Asset Optimization Specifications](#5-asset-optimization-specifications)
- [6. Cache Invalidation Strategy](#6-cache-invalidation-strategy)
- [7. Security & Compliance Policies](#7-security--compliance-policies)
- [8. Observability & Monitoring](#8-observability--monitoring)
- [9. Diagnostic & Troubleshooting](#9-diagnostic--troubleshooting)

---

### 1. Executive Summary

This repository provides a Content Delivery Network (CDN) infrastructure for distributing static assets used in modern web applications and digital products with ultra-low latency across the globe.

By leveraging GitHub as the origin storage and utilizing jsDelivr's multi-CDN network (Cloudflare, Fastly, Bunny CDN, etc.), we achieve enterprise-grade reliability and performance.

---

### 2. Core Capabilities & SLAs

#### 🎯 Core Principles

##### 1. High Availability
- Automatic failover via multi-CDN
- Immediate routing switchover during outages
- SLA: 99.99% Uptime

##### 2. Immutability
- Complete fixation via Git commit hash or SemVer
- Prevention of cache poisoning

##### 3. Performance Optimization
- Brotli / Gzip compression
- HTTP/2 / HTTP/3 support
- Long-term cache strategy

##### 4. Global Edge Delivery
- Distribution from edge locations worldwide
- Shortest path routing

---

### 3. Integration Guidelines

#### 3.1 CDN URL Scheme

```text
https://cdn.jsdelivr.net/gh/{username}/{repo}@{version}/{path}
```

#### 3.2 Implementation Example (Next.js)

```ts
export const CDN_BASE_URL = "https://cdn.jsdelivr.net/gh/Username/Repo@main";
```

```tsx
<link rel="preconnect" href="https://cdn.jsdelivr.net" crossOrigin="anonymous" />
<link rel="stylesheet" href={`${CDN_BASE_URL}/styles/main.min.css`} />
```

---

#### 3.3 AI Model Delivery

```ts
import { pipeline, env } from "@xenova/transformers";

env.localModelPath = "https://cdn.jsdelivr.net/gh/Username/Repo@main/assets/models/";

const classifier = await pipeline("sentiment-analysis", "custom-model");
```

---

### 4. Directory Architecture & Typology

```plaintext
/
├── assets/
│   ├── images/
│   │   ├── branding/
│   │   └── ui/
│   ├── models/
│   │   ├── onnx/
│   │   └── safetensors/
│   ├── scripts/
│   │   ├── core/
│   │   └── ai-workers/
│   ├── styles/
│   │   ├── tailwind/
│   │   └── design-systems/
│   └── typography/
│       ├── product-sans/
│       └── display/
├── docs/
├── .github/
└── README.md
```

---

### 5. Asset Optimization Specifications

#### 5.1 Typography
- Use .woff2 only
- Subsetting required

#### 5.2 Images
- WebP / AVIF recommended
- SVG optimization

#### 5.3 AI Models
- int8 / uint8 quantization
- 50MB or less (split if larger)

#### 5.4 Naming Rules

```text
[a-z0-9-]
```

---

### 6. Cache Invalidation Strategy

#### Recommended: Cache Busting
```
@v1.0.0 → @v1.0.1
```

#### Forced Purge

```bash
curl https://purge.jsdelivr.net/gh/Username/Repo@main/file.css
```

---

### 7. Security & Compliance Policies

#### No Secrets Policy
- API keys forbidden
- Passwords forbidden

#### CORS

```http
Access-Control-Allow-Origin: *
```

---

### 8. Observability & Monitoring

#### Verification Items
- Latency
- Cache hit ratio

#### Debugging

```http
x-cache: HIT / MISS
```

---

### 9. Diagnostic & Troubleshooting

#### 404 Not Found
- Verify version
- Check path

#### 403 Forbidden
- Verify size limit (50MB)

#### Slow Performance
- Confirm first-time MISS
- Verify HIT on reaccess

---

### 👨‍💻 Maintainers
Core Systems Engineering Team

---

### 📄 License
MIT License
