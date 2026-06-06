<div align="center">

<img src="https://img.shields.io/badge/Platform-Android%208.0%2B-00e5ff?style=for-the-badge&logo=android&logoColor=black" />
<img src="https://img.shields.io/badge/Language-Kotlin-8b5cf6?style=for-the-badge&logo=kotlin&logoColor=white" />
<img src="https://img.shields.io/badge/UI-Jetpack%20Compose-00ff88?style=for-the-badge&logo=jetpackcompose&logoColor=black" />
<img src="https://img.shields.io/badge/Encryption-AES--256--GCM-00e5ff?style=for-the-badge&logo=gnuprivacyguard&logoColor=black" />
<img src="https://img.shields.io/badge/License-MIT-8b5cf6?style=for-the-badge" />
<img src="https://img.shields.io/badge/Version-v1.0.0-00ff88?style=for-the-badge" />

<br/><br/>

```
 ██████╗██████╗ ██╗   ██╗██████╗ ████████╗ ██████╗ ████████╗ █████╗ ██╗     ██╗  ██╗
██╔════╝██╔══██╗╚██╗ ██╔╝██╔══██╗╚══██╔══╝██╔═══██╗╚══██╔══╝██╔══██╗██║     ██║ ██╔╝
██║     ██████╔╝ ╚████╔╝ ██████╔╝   ██║   ██║   ██║   ██║   ███████║██║     █████╔╝ 
██║     ██╔══██╗  ╚██╔╝  ██╔═══╝    ██║   ██║   ██║   ██║   ██╔══██║██║     ██╔═██╗ 
╚██████╗██║  ██║   ██║   ██║        ██║   ╚██████╔╝   ██║   ██║  ██║███████╗██║  ██╗
 ╚═════╝╚═╝  ╚═╝   ╚═╝   ╚═╝        ╚═╝    ╚═════╝    ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝
```

### **Privacy-First · Zero-Trust · Secure Mobile Messaging**

*Where even the server is treated as a potential adversary.*

<br/>

[**⬇ Download APK**](https://github.com/karan942006/CryptoTalkApp/releases/download/CryptoTalk/app-debug.apk) · [**📋 View Releases**](https://github.com/karan942006/CryptoTalkApp/releases) · [**🐛 Report Bug**](https://github.com/karan942006/CryptoTalkApp/issues) · [**🔒 Security Disclosure**](https://github.com/karan942006/CryptoTalkApp/security)

</div>

---

## 🔐 What is CryptoTalk?

CryptoTalk is a **zero-trust encrypted messaging platform** for Android, engineered around a single principle: **your conversations belong to you alone — not to servers, not to corporations, not to anyone.**

Most "secure" apps treat privacy as a feature. CryptoTalk treats it as the architecture.

Built from the ground up with **hardware-backed cryptography**, a **functional disguise system**, and a **one-tap panic wipe** — CryptoTalk brings enterprise-grade security to everyday users.

```
$ init --keystore android_hardware_tee
✓ RSA-2048 KeyPair generated in hardware TEE
✓ AES/GCM/NoPadding cipher armed (256-bit)
⚠ Root binary detected → Integrity shield raised
✓ Disguise: CALCULATOR mode active
```

---

## ✨ Feature Overview

### 🔐 01 · Secure Messaging & Encryption

| Feature | Details |
|---|---|
| **Hybrid Encryption Engine** | RSA-2048 for key exchange + AES-256-GCM for message content. Every message uses a unique randomly generated 256-bit AES key. |
| **Android Keystore (TEE)** | Private keys are stored exclusively in the Android Hardware Keystore. Keys never leave the physical device. Decryption never exits the secure enclave. |
| **Perfect Forward Secrecy** | Fresh AES keys and unique IVs are generated per message via CSRNG. Compromise of one session key affects nothing else. |
| **Real-Time Messaging UI** | Full reactive chat interface with live updates, message state indicators, and conversation management — built with Jetpack Compose. |

---

### 🎭 02 · Stealth & Disguise Mode

> *Conventional messengers protect message content. CryptoTalk also protects the context of the app's existence on your device.*

| Mode | UI | Unlock Method |
|---|---|---|
| 🧮 **Calculator** | Fully functional arithmetic calculator — a real decoy, not a blank screen | Enter code + press `=` |
| 🌤 **Weather** | Live weather display with real location data | Tap temperature × 5 rapidly |
| 🔐 **CryptoTalk** | Standard app identity for trusted environments | Via Disguise Settings Panel |

**How it works:** Uses `<activity-alias>` entries in `AndroidManifest.xml`. `DisguiseManager.kt` calls the system `PackageManager` to disable the real launcher and enable a fake alias — **persisting across app updates and device reboots**.

```kotlin
// DisguiseManager.kt — alias switching
packageManager.setComponentEnabledSetting(
    realLauncherComponent,
    COMPONENT_ENABLED_STATE_DISABLED, DONT_KILL_APP
)
packageManager.setComponentEnabledSetting(
    calculatorAliasComponent,
    COMPONENT_ENABLED_STATE_ENABLED, DONT_KILL_APP
)
```

---

### 🛡 03 · Advanced Security & Data Protection

| Feature | Details |
|---|---|
| **💥 Panic Wipe** | One-tap kill switch: destroys local SQLite DB, Keystore-backed passphrases, Firebase sessions, and all cache. No forensic trace remains. |
| **🧬 Biometric Gate** | Fingerprint/Face unlock independent of the device's screen lock — the app stays locked even if the phone itself is unlocked. |
| **🛡 App Integrity** | Runtime APK signature verification detects tampered or re-signed builds before any crypto operations execute. |
| **🔑 Safety Numbers** | Out-of-band public key fingerprint comparison to prevent Man-in-the-Middle attacks. |
| **🚫 FLAG_SECURE** | OS-level screenshot and screen recording is blocked system-wide across all app screens. |
| **🔍 Hook Detection** | Detects Frida, Xposed, and debugger attachment at runtime — raises integrity shield automatically. |

---

### 👤 04 · User Identity & Customization

| Feature | Details |
|---|---|
| **Dynamic Profile** | Real-time display name, bio, and status sync to Firestore instantly. |
| **Contact Nicknames** | Local-only private aliases for contacts — never synced to server, never matching your address book. |
| **Dark Theme Engine** | Cyber-noir dark theme with Xiaomi/MIUI specific rendering optimizations. |

---

## 🏗 Architecture

CryptoTalk uses **MVVM + Clean Architecture** with strict separation of concerns:

```
┌─────────────────────────────────────────────┐
│          VIEW — Jetpack Compose UI          │  ← "Dumb" display layer. No business logic.
├─────────────────────────────────────────────┤
│      VIEWMODEL — Lifecycle-Aware Brain      │  ← StateFlow + Coroutines. Survives rotation.
├─────────────────────────────────────────────┤
│       REPOSITORY — Single Source of Truth   │  ← AuthRepo · MessageRepo · UserRepo
├─────────────────────────────────────────────┤
│     CRYPTO ENGINE — MessageCrypto.kt        │  ← AES keygen · GCM encrypt · RSA wrap
├─────────────────────────────────────────────┤
│   Firebase Firestore + Google OAuth Auth    │  ← Treated as zero-trust encrypted relay
└─────────────────────────────────────────────┘
```

### Firestore Payload (Zero Plaintext Server)

The server never sees readable data — only opaque encrypted blobs:

```json
{
  "ciphertext": "Qx9p+fE2wR4mKo7n...",
  "iv": "base64_12_byte_nonce",
  "participantKeys": {
    "userA": "RSA_wrapped_AES_key_A",
    "userB": "RSA_wrapped_AES_key_B"
  }
}
```

---

## 🔑 Cryptographic Engine

### The Lifecycle of an Encrypted Message

```
[Plaintext] → [CSRNG: AES-256 Key + 12B IV] → [AES/GCM Encrypt]
     → [RSA Wrap per recipient] → [Firestore (ciphertext only)]
          → [TEE RSA Unwrap] → [GCM Auth Tag Verify] → [Plaintext]
```

### AES/GCM — Why Not CBC?

```
CBC  ✗  Vulnerable to Padding Oracle Attacks. No integrity guarantee.
GCM  ✓  AEAD: Confidentiality + Integrity + Authenticity in one pass.
         128-bit authentication tag appended to every ciphertext.
         Single-bit modification → decryption aborts immediately.
```

### Key Code Snippets

```kotlin
// MessageCrypto.kt — AES/GCM/NoPadding
val cipher = Cipher.getInstance("AES/GCM/NoPadding")
val spec = GCMParameterSpec(128, iv)  // 128-bit authentication tag
cipher.init(Cipher.ENCRYPT_MODE, aesKey, spec)
// Result: confidentiality + integrity + authenticity simultaneously
```

```kotlin
// KeystoreHelper.kt — RSA keypair in Hardware TEE
val gen = KeyPairGenerator.getInstance(
    KeyProperties.KEY_ALGORITHM_RSA, "AndroidKeyStore"
)
gen.initialize(
    KeyGenParameterSpec.Builder(alias, PURPOSE_ENCRYPT or PURPOSE_DECRYPT)
        .setKeySize(2048)
        .setDigests(DIGEST_SHA256)
        .build()
)
// Private key: hardware-bound and cryptographically non-extractable
```

---

## 🎯 Threat Model

| Threat | CryptoTalk's Mitigation |
|---|---|
| 🕵 **Metadata Harvesting** | Minimized Firestore schema. Zero plaintext metadata stored. Data minimization by design. |
| ☁ **Cloud Cleartext Backup** | Zero-knowledge server. Firebase mathematically cannot read any stored data. |
| 🔓 **Software Key Storage** | Android Keystore TEE. Private key is hardware-bound and non-extractable even on rooted devices. |
| 👁 **Physical Device Access** | Disguise Mode hides the app's identity. Biometric Gate locks it independently of screen lock. |
| 🎯 **Man-at-the-Endpoint** | FLAG_SECURE blocks OS-level capture. IntegrityCheck detects Frida, Xposed, and debugger hooks. |
| 🚨 **Forced Device Seizure** | Panic Wipe: Firebase logout + DB deletion + cache purge + process kill in a single action. |

---

## ⚔ Comparison

| Feature | **CryptoTalk** | Signal | Telegram | WhatsApp |
|---|:---:|:---:|:---:|:---:|
| End-to-End Encryption | ✅ Always | ✅ Always | ⚠️ Secret Chats only | ✅ Always |
| **Disguise / Stealth Mode** | ✅ Icon + Name + Fake UI | ❌ | ❌ | ❌ |
| **Emergency Panic Wipe** | ✅ Immediate destruction | ❌ | ❌ | ❌ |
| Hardware Key Storage | ✅ Android Keystore TEE | ⚠️ Filesystem | ⚠️ Local | ⚠️ Local |
| **App Integrity Verification** | ✅ Built-in APK check | ❌ | ❌ | ❌ |
| Safety Numbers (MITM) | ✅ | ✅ | ❌ | ⚠️ Limited |
| Phone Number Required | ❌ Pseudonyms supported | ✅ Required | ⚠️ Optional | ✅ Required |
| No Ads / No Tracking | ✅ | ✅ | ⚠️ | ❌ |

---

## 🗺 Roadmap

```
✅ SHIPPED    Hybrid Encryption Engine (RSA-2048 + AES-256-GCM + Hardware TEE)
✅ SHIPPED    Disguise Mode + Panic Wipe + Biometric Gate
✅ SHIPPED    Integrity Shield + FLAG_SECURE + Safety Numbers

🔵 PHASE 1   Encrypted Media + Self-Destructing Messages (TTL-based auto-vanish)
🔵 PHASE 2   Encrypted Group Chats + Secure Multi-Device Sync (QR key sharing)
🟣 PHASE 3   Remote Wipe + Desktop Client (Rust) + Metadata Obfuscation
🟣 FUTURE    Post-Quantum Cryptography (Kyber/NIST PQC) + Decentralized Identity (DID)
```

---

## 📦 Installation

### Option 1 — Direct APK Download

1. Download the latest APK from [**GitHub Releases**](https://github.com/karan942006/CryptoTalkApp/releases/download/CryptoTalk/app-debug.apk)
2. On your Android device, enable **"Install from Unknown Sources"** in Settings
3. Open the downloaded APK and install

### Option 2 — Build from Source

```bash
# Clone the repository
git clone https://github.com/karan942006/CryptoTalkApp.git
cd CryptoTalkApp

# Add your google-services.json to /app directory
# (Firebase project required for Firestore + Auth)

# Build debug APK
./gradlew assembleDebug

# Output: app/build/outputs/apk/debug/app-debug.apk
```

**Requirements:**
- Android 8.0+ (API 26+)
- Android Studio Hedgehog or newer
- JDK 17+

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin 1.9 |
| UI | Jetpack Compose |
| Architecture | MVVM + Clean Architecture |
| Async | Kotlin Coroutines + StateFlow |
| Encryption | Android Keystore · AES/GCM · RSA-2048 |
| Backend | Firebase Firestore + Firebase Auth |
| Auth | Google OAuth 2.0 |
| Local DB | Room (SQLite) |
| DI | Hilt |

---

## 👥 Team

<table>
<tr>
<td align="center"><b>Shaila Mandkulkar</b><br/><sub>Co-Founder · Security</sub><br/><sub>Cryptography architecture & threat modeling. Designed the zero-trust security framework.</sub></td>
<td align="center"><b>Karan Lingayat</b><br/><sub>Co-Founder · Android</sub><br/><sub>Android Keystore TEE integration & encryption pipeline. Built the core crypto engine.</sub></td>
<td align="center"><b>Parth Kelaskar</b><br/><sub>Co-Founder · UI/UX</sub><br/><sub>Jetpack Compose UI, disguise mode UX, and the premium dark theme engine.</sub></td>
</tr>
</table>

---

## 📄 License

```
MIT License — Copyright © 2026 CryptoTalk

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software to use, copy, modify, merge, publish, distribute, sublicense,
and/or sell copies — subject to the MIT License terms.
```

---

<div align="center">

**Privacy is a fundamental human right. CryptoTalk is our contribution to that principle.**

<br/>

Made with 🔐 by **Shaila Mandkulkar · Karan Lingayat · Parth Kelaskar**

<br/>

<img src="https://img.shields.io/badge/Zero%20Plaintext%20on%20Server-%E2%9C%93-00ff88?style=flat-square" />
<img src="https://img.shields.io/badge/No%20Ads-%E2%9C%93-00ff88?style=flat-square" />
<img src="https://img.shields.io/badge/No%20Tracking-%E2%9C%93-00ff88?style=flat-square" />
<img src="https://img.shields.io/badge/Free%20Forever-%E2%9C%93-00ff88?style=flat-square" />
<img src="https://img.shields.io/badge/Open%20Source-%E2%9C%93-00ff88?style=flat-square" />

</div>
