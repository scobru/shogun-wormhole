# 🌌 WORMHOLE

A high-performance, decentralized P2P and IPFS file transfer tool using ZEN. WORMHOLE provides end-to-end encrypted sharing through both a CLI interface and a modern web dashboard.

## 🚀 Overview

WORMHOLE uses a hybrid architecture for reliable and privacy-focused file transmission:
- **ZEN Protocol**: For real-time metadata exchange, presence, status synchronization, and decentralized identity.
- **WebRTC Direct Stream**: High-throughput peer-to-peer file streaming directly between clients.
- **IPFS Relay**: Staged decentralized hosting of encrypted chunks when direct P2P is unavailable.
- **E2E Encryption**: All files are encrypted on the client using AES-GCM before transmission.
- **Local Discovery**: Automatic peer finding on local networks via UDP Multicast.

---

## 🛠️ Features

- 🔐 **End-to-End Secure (E2EE)**: Files are encrypted client-side using the mnemonic code as the encryption key.
- ⚡ **Direct P2P & IPFS Relay**: Choose between direct WebRTC streaming or decentralized relay staging.
- 📦 **Shared Core**: Identical transfer and crypto logic across CLI and Web for consistent behavior.
- 🔗 **Mnemonic Codes**: Simple, human-readable sharing codes (e.g., `5-brave-fire`).
- 🏎️ **LAN Discovery**: Super-fast peer discovery on local networks using Multicast (UDP).
- 🔄 **Auto Cleanup**: Files are automatically unpinned and metadata cleared after transfer completion.

---

## 💻 CLI Interface

### Installation

```bash
# Global installation
npm install -g wormhole

# Or run instantly with npx
npx wormhole send <file-path>
```

### Commands

| Command | Description |
|---------|-------------|
| `wormhole send <file>` | Encrypts and sends a file via P2P (or `--ipfs` for relay), generating a sync code. |
| `wormhole receive <code>` | Downloads and decrypts a file using the provided code. |
| `wormhole list` | Lists currently active transfers (experimental). |

---

## 🌐 Web Application

### Local Development

1. Navigate to the web directory:
   ```bash
   cd web
   yarn install
   ```

2. Start the development server:
   ```bash
   yarn dev
   ```

The web interface will be available at `http://localhost:5173` (default Vite port).

---

## 🏗️ Project Structure

```text
wormhole/
├── src/
│   ├── index.js              # CLI Application (send, receive, list)
│   └── core.js               # CLI proxy for shared transfer logic
├── web/
│   ├── src/
│   │   ├── shared/
│   │   │   └── wormhole-core.js # SHARED LOGIC (Encryption, ZEN, WebRTC, IPFS)
│   │   └── main.js           # Frontend Logic & UI Controller
│   ├── styles/
│   │   └── wormhole.css      # Design System, Glassmorphism & Custom Styling
│   └── index.html            # Web Entry Point
├── package.json              # Main project config and CLI binary
└── README.md                 # Project Documentation
```

---

## ⚙️ Configuration

The application uses environment variables for relay and authorization configuration.

| Variable | Description |
|----------|-------------|
| `VITE_RELAY_URL` | The URL of the IPFS relay. |
| `VITE_AUTH_TOKEN` | Bearer token for authorized upload access to the relay. |

---

## 🛡️ Security & Privacy

1. **Protocol Isolation**: Relays and network peers only see encrypted chunks; they never see filenames, plaintext content, or keys.
2. **Deterministic Keys**: Cryptographic keys are derived from the mnemonic code using PBKDF2/AES-GCM.
3. **No Central Logs**: All peer coordination happens on the decentralized ZEN network.
4. **Instant Cleanup**: Successful transfers trigger an `unpin` request to the IPFS relay.

---

Built with ❤️ by [scobru](https://github.com/scobru).  
*Securing the decentralized web, one chunk at a time.*
