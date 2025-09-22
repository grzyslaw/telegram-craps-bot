# Telegram Craps Bot – On-Chain Casino Prototype

This project is a **Telegram bot frontend** for a fully on-chain implementation of the classic [**Craps** dice game](https://en.wikipedia.org/wiki/Craps#Rules_of_play), extended with a unique **Arena mode** for competitive play.  

The bot integrates wallet management, secure password-based access, an analytics/leaderboard layer, and a smooth Telegram experience on top of a **Solidity smart contract backend** that enforces game rules and payouts.  

⚠️ **Disclaimer**: The underlying code is proprietary and not published here.  
This repo is meant as a **case study showcase**. A **demo video** is provided, and the bot can be spun up **on demand for live testing**. 

---

## 🎥 Demo

[▶️ Watch the bot in action](https://youtu.be/7vhqAQOKsKU)  

---

## 🎮 Gameplay Features

- **Solo Mode**:  
  - Fully on-chain implementation of Craps with all major bet types:
    - Pass / Don’t Pass, Come / Don’t Come  
    - Field, Place, Lay bets  
    - Hardways, Craps, Seven  
    - Bonus bets (All/Tall/Small, Fire bet, Repeaters, Hot Roller)  

- **Arena Mode (1v1)**:  
  - Two players compete in timed **3-minute** matches.  
  - Each starts with **100 credits**.  
  - Winner = highest balance after time expires or all bets conclude.  
  - Daily free games limit with tracking of wins/losses/draws.  

---

## 🔐 Non-Game Features

- **Wallet Management**  
  - Create a wallet (mnemonic generation).  
  - Import existing wallet with mnemonic.  

- **Password-Protected Accounts**  
  - User sessions secured with a password.  
  - Session expiry + re-authentication.  
  - Secure encryption with:
    - `ciphersweet-js` (encrypted storage of mnemonics/passwords).  
    - `scrypt` key derivation + SHA-256 hashing.  
    - Backend key combined with user password for layered protection.  

- **Telegram UX**  
  - Virtual craps board rendered directly in chat.  
  - Errors and invalid actions clearly displayed.  
  - Smooth flow between solo and Arena modes.  

---

## 📊 Analytics & Leaderboards (PostgreSQL) 

- **Metrics exposed**:
  - **User PnL** over configurable time ranges.  
  - **User ranking/position** vs everyone in the same window.  
  - **PnL over time series** (bucketing by interval).  
  - **Global PnL over time**.  
  - **Leaderboard** for Arena wins/losses.  

**Privacy & security notes:**
- Mnemonics are **encrypted at rest** (CipherSweet) and only decrypted with a key derived from **user password + backend key**.  
- No plaintext mnemonics stored; passwords are never stored in plaintext.  
- DB is used for **analytics and UX**; **on-chain state remains the source of truth** for balances/payouts.

---

## 🛠 Technical Highlights

- **Smart Contracts**  
  - Solidity Craps logic (bet resolution, dice rolls).  
  - Arena extension with matchmaking, timers, and credit balances.  
  - Event-driven architecture for bet resolution and match outcomes.  

- **Bot Backend**  
  - Node.js + TypeScript.  
  - Telegram Bot API integration.  
  - User session + password management with encrypted DB storage.  

- **Deployment**  
  - CI/CD with **GitHub Actions** (self-hosted runner):  
    - Build & test contracts with Foundry.  
    - Deploy contracts to testnet.  
    - Generate configs and push to VPS.  
    - Restart bot & listener.  
  - Hosted on self-managed VPS.  

- **Testing**  
  - Contracts fully tested in **Foundry**.  
  - Telegram bot tested manually in real chat environment.  

---

## 👤 My Role

- Both **smart contracts** and **Telegram bot backend**.  
- Entire **Craps game logic** from scratch in Solidity.  
- Wallet encryption, Telegram integration, analytics, and co-worked on CI/CD.    

---

## 🚧 Status

This was developed as part of a client project.  
- **Code is not open-source.**  
- **Demo video is available.**   

---

## 🔑 Tech Stack
- **Solidity** – on-chain Craps + Arena contracts  
- **Foundry (Forge)** – contract testing and deployment  
- **Node.js / TypeScript** – Telegram bot backend + event listener  
- **PostgreSQL** – analytics, PnL, leaderboards  
- **ciphersweet-js, scrypt, crypto** – encryption & password handling  
- **Telegram Bot API** – user interface  
- **GitHub Actions + pm2 + VPS** – CI/CD and hosting  

--- 
