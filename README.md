# 🧠 Secure Notepad – Blockchain-Based Encrypted Notepad

A simple and beginner-friendly **Solidity smart contract** that lets users create, update, share, and store notes securely on the blockchain.  
This project demonstrates ownership, access control, and event-driven smart contract design — making it an excellent starting point for new blockchain developers.

---

## 💡 Project Description

**Secure Notepad** is a decentralized notepad built on the Ethereum blockchain.  
It allows users to write, edit, share, and manage their notes directly on-chain, ensuring transparency, immutability, and user ownership.

> ⚠️ **Note:** Blockchain data is public.  
> For real privacy, you should **encrypt notes off-chain** or store them on **IPFS** and save only the CID in the contract.

---

## 🚀 What It Does

- 📝 **Create Notes:** Store encrypted note data or IPFS links on the blockchain.  
- ✏️ **Update Notes:** Modify your own notes at any time.  
- 🔐 **Share Access:** Grant or revoke read access to specific Ethereum addresses.  
- ❌ **Delete Notes:** Mark notes as deleted while keeping history transparent.  
- 👀 **Read Notes:** Retrieve content if you’re the owner or have been granted access.  
- ⏱️ **Timestamps:** Automatically records creation and update times for every note.

---

## 🌟 Features

| Feature | Description |
|----------|-------------|
| 🧾 **Note Struct** | Each note has a unique ID, owner, timestamps, and content field. |
| 🔑 **Ownership Control** | Only the creator (owner) can update or delete their notes. |
| 🤝 **Sharing System** | Owners can grant/revoke read permissions for others. |
| 🕵️ **Privacy Support** | Store ciphertext or IPFS CID instead of plaintext data. |
| 📢 **Events** | Emits `NoteCreated`, `NoteUpdated`, `NoteDeleted`, and `NoteShared` events for front-end tracking. |
| 🧠 **Learning Focused** | Easy to read, simple to extend, and ideal for Solidity beginners. |

---

## 🔗 Deployed Smart Contract Link

**Network:** Sepolia Testnet  
**Contract Address/Transaction:**  
[https://sepolia.celoscan.io/tx/0x8f4b763d297c9becd4a9e7d4690d29396ffa7b43ca1b3e35df96346a4ce0318a](https://sepolia.celoscan.io/tx/0x8f4b763d297c9becd4a9e7d4690d29396ffa7b43ca1b3e35df96346a4ce0318a)

---

## 💻 Smart Contract Code

```solidity
//paste your code
