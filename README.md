# 🎓 CredSure - Blockchain-Powered Credential Verification

<div align="center">

**A decentralized platform for issuing, storing, and verifying academic credentials on the Polygon blockchain**

[Live Demo](https://credsure.siddz.com) • [Report Bug](https://github.com/SiddDevZ/credsure/issues) • [Request Feature](https://github.com/SiddDevZ/credsure/issues)

</div>

---

## 📸 Screenshot

<div align="center">
  <img src="./screenshot.png" alt="CredSure Platform Screenshot" width="100%">
</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Environment Variables](#environment-variables)
  - [Running the Application](#running-the-application)
- [Project Structure](#-project-structure)
- [How It Works](#-how-it-works)
- [API Documentation](#-api-documentation)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

**CredSure** is a blockchain-powered platform that revolutionizes academic credential verification. Built on the Polygon network, it enables universities to issue tamper-proof certificates, allows students to own and share their achievements securely, and provides recruiters with instant, fraud-proof verification.

### The Problem

- 🕐 Traditional credential verification takes days or weeks
- 🔓 Academic fraud and fake certificates are widespread
- 💰 Manual verification processes are expensive and inefficient
- 📄 Students don't truly own their academic achievements
- 🌍 Cross-border credential verification is complex

### The Solution

CredSure leverages blockchain technology to create an immutable, decentralized system where:
- ✅ Credentials are hashed and stored on the Polygon blockchain
- ⚡ Verification happens in seconds, not days
- 🔒 Tamper-proof security ensures authenticity
- 👤 Students maintain complete ownership of their credentials
- 🌐 Global recognition across institutions and borders

---

## ✨ Features

### For Universities 🏛️
- **Issue Credentials**: Upload and issue certificates with blockchain verification
- **Manage Students**: Track all issued credentials in a centralized dashboard
- **Instant Publishing**: Credentials are hashed and stored on-chain immediately
- **Authentication System**: Secure login with JWT tokens

### For Students 🎓
- **Digital Vault**: Store all credentials in one secure location
- **QR Code Sharing**: Generate shareable QR codes for instant verification
- **Selective Sharing**: Choose what information to share and with whom
- **Download Options**: Export credentials as PDFs or images
- **Real-time Updates**: See verification status and blockchain confirmations

### For Recruiters/Verifiers 🔍
- **Instant Verification**: Validate credentials in seconds via QR scan or upload
- **Blockchain Proof**: See transaction hashes and on-chain verification
- **Fraud Prevention**: Tamper-proof system prevents fake credentials
- **No Registration Required**: Public verification page for anyone

### Technical Features ⚙️
- **Blockchain Integration**: Polygon (Amoy testnet) for low-cost, fast transactions
- **Smart Hashing**: SHA-256 cryptographic hashing for credential integrity
- **RESTful API**: Complete backend API with Hono.js
- **Modern UI**: Beautiful, responsive design with Tailwind CSS
- **Animation Effects**: Smooth transitions using Framer Motion
- **QR Code Generation**: Easy sharing and verification
- **File Upload**: Support for PDF, image, and document formats

---

## 🛠️ Tech Stack

### Frontend
- **Framework**: [Next.js 15](https://nextjs.org/) - React framework with App Router
- **Language**: JavaScript (JSX)
- **Styling**: [Tailwind CSS 4](https://tailwindcss.com/) - Utility-first CSS framework
- **UI Components**: 
  - [Radix UI](https://www.radix-ui.com/) - Accessible component primitives
  - Custom magic UI components (animated effects)
  - [Lucide Icons](https://lucide.dev/) - Beautiful icon library
- **Animations**: 
  - [Framer Motion](https://www.framer.com/motion/) - Production-ready motion library
  - [Lenis](https://github.com/studio-freight/lenis) - Smooth scroll library
- **Notifications**: [Sonner](https://sonner.emilkowal.ski/) - Toast notifications
- **QR Codes**: QR code generation for credential sharing

### Backend
- **Framework**: [Hono.js](https://hono.dev/) - Ultrafast web framework
- **Runtime**: Node.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (JSON Web Tokens)
- **File Upload**: Multipart form data handling
- **Static Files**: Serve uploaded credentials

### Blockchain
- **Network**: Polygon Amoy Testnet
- **Library**: [ethers.js v6](https://docs.ethers.org/v6/) - Ethereum interaction library
- **Smart Contracts**: Hardhat development environment
- **Hashing**: SHA-256 cryptographic hashing
- **Storage Method**: Transaction data field storage

### DevOps
- **Package Manager**: npm
- **Linting**: ESLint
- **Build Tool**: Next.js Turbopack
- **Version Control**: Git

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         Frontend (Next.js)                       │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │   Student    │  │  University  │  │   Validate   │          │
│  │  Dashboard   │  │  Dashboard   │  │     Page     │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└─────────────────────────────────┬───────────────────────────────┘
                                  │ API Calls (REST)
┌─────────────────────────────────┼───────────────────────────────┐
│                         Backend (Hono.js)                        │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Routes: /api/student | /api/university | /api/credentials│  │
│  └──────────────────────────────────────────────────────────┘   │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │ Auth Middle- │  │   Models     │  │   Blockchain │          │
│  │    ware      │  │  (Mongoose)  │  │   Service    │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
└─────────────────────────────────┬───────────────────────────────┘
                                  │
              ┌───────────────────┼───────────────────┐
              │                   │                   │
         ┌────▼────┐      ┌──────▼──────┐   ┌───────▼────────┐
         │ MongoDB │      │   Polygon   │   │  File Storage  │
         │Database │      │  Blockchain │   │  (uploads/)    │
         └─────────┘      └─────────────┘   └────────────────┘
```

### Data Flow

1. **Credential Issuance**:
   ```
   University → Upload Certificate → Backend validates
   → Generate SHA-256 hash → Store in MongoDB
   → Send hash to Polygon blockchain → Return transaction hash
   → Student receives credential
   ```

2. **Credential Verification**:
   ```
   Verifier → Upload/Scan Credential → Backend retrieves hash
   → Query blockchain for matching transaction
   → Return verification status + blockchain proof
   ```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** >= 18.0.0
- **npm** or **yarn** or **pnpm**
- **MongoDB** (local or Atlas)
- **Polygon Amoy Testnet** account with test MATIC

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/SiddDevZ/credsure-hackathon.git
   cd credsure-hackathon
   ```

2. **Install frontend dependencies**
   ```bash
   npm install
   ```

3. **Install backend dependencies**
   ```bash
   cd Backend
   npm install
   cd ..
   ```

### Environment Variables

#### Backend (.env in `Backend/` directory)

```env
# Database
DATABASE_URL=mongodb://localhost:27017/credsure
# or MongoDB Atlas
# DATABASE_URL=mongodb+srv://username:password@cluster.mongodb.net/credsure

# Blockchain
POLYGON_AMOY_RPC_URL=https://rpc-amoy.polygon.technology/
PRIVATE_KEY=your_wallet_private_key_without_0x

# JWT Secret
JWT_SECRET=your_super_secret_jwt_key_here

# Server
PORT=3001
```

#### Frontend (update `config.json` in root directory)

```json
{
  "backend_url": "http://localhost:3001",
  "frontend_url": "http://localhost:3000"
}
```

### Running the Application

#### Development Mode

1. **Start the backend server**
   ```bash
   cd Backend
   npm start
   ```
   Backend will run on `http://localhost:3001`

2. **Start the frontend** (in a new terminal)
```bash
npm run dev
   ```
   Frontend will run on `http://localhost:3000`

#### Production Build

1. **Build the frontend**
   ```bash
   npm run build
   npm start
   ```

2. **Run the backend**
   ```bash
   cd Backend
   npm start
   ```

---

## 📁 Project Structure

```
credsure-hackathon/
├── app/                          # Next.js App Router
│   ├── layout.jsx               # Root layout
│   ├── page.jsx                 # Landing page
│   ├── globals.css              # Global styles
│   ├── student/                 # Student routes
│   │   ├── login/              # Student login
│   │   ├── register/           # Student registration
│   │   └── dashboard/          # Student dashboard
│   ├── university/             # University routes
│   │   ├── login/              # University login
│   │   ├── register/           # University registration
│   │   └── dashboard/          # University dashboard (issue credentials)
│   └── validate/               # Public verification page
├── components/                  # React components
│   ├── Navbar.jsx              # Navigation bar
│   ├── Footer.jsx              # Footer
│   ├── Reviews.jsx             # Reviews section
│   ├── FaqSection.jsx          # FAQ component
│   ├── SmoothScrolling.jsx     # Smooth scroll wrapper
│   ├── magicui/                # Animated UI components
│   └── ui/                     # Reusable UI components
├── lib/                        # Utilities
│   ├── config.js               # Configuration loader
│   └── utils.js                # Helper functions
├── Backend/                    # Backend server
│   ├── server.js              # Main server file (Hono.js)
│   ├── models/                # MongoDB models
│   │   ├── Student.js         # Student schema
│   │   ├── University.js      # University schema
│   │   └── Credential.js      # Credential schema
│   ├── routes/                # API routes
│   │   ├── studentAuth.js     # Student authentication
│   │   ├── universityAuth.js  # University authentication
│   │   └── credentialRoutes.js # Credential CRUD operations
│   ├── middleware/            # Custom middleware
│   │   ├── studentAuthMiddleware.js
│   │   └── universityAuthMiddleware.js
│   ├── utils/                 # Backend utilities
│   │   ├── blockchain.js      # Blockchain service (ethers.js)
│   │   └── tokenGenerator.js  # JWT token generation
│   ├── uploads/               # Uploaded credential files
│   └── package.json           # Backend dependencies
├── scripts/                   # Utility scripts
│   └── deploy.js             # Hardhat deployment script
├── public/                    # Static assets
│   ├── universities/          # University logos
│   └── *.svg                 # Icons and images
├── hardhat.config.js         # Hardhat configuration
├── config.json               # App configuration (URLs)
├── components.json           # shadcn/ui configuration
├── tailwind.config.ts        # Tailwind CSS configuration
├── next.config.mjs           # Next.js configuration
├── package.json              # Frontend dependencies
└── README.md                 # This file
```

---

## 💡 How It Works

### 1. University Issues Credential

```mermaid
sequenceDiagram
    University->>Backend: Upload certificate + student info
    Backend->>Backend: Generate SHA-256 hash
    Backend->>MongoDB: Store credential metadata
    Backend->>Polygon: Send transaction with hash
    Polygon-->>Backend: Transaction hash
    Backend-->>University: Credential issued ✅
    Backend->>Student: Credential available in dashboard
```

### 2. Student Views & Shares Credential

- Student logs in and sees all their credentials
- Can generate QR code with credential slug
- Can download credential as PDF/image
- Shares QR code or link with recruiters

### 3. Recruiter Verifies Credential

```mermaid
sequenceDiagram
    Recruiter->>Frontend: Scan QR / Upload file
    Frontend->>Backend: Send credential identifier
    Backend->>MongoDB: Fetch credential metadata
    Backend->>Polygon: Search blockchain for hash
    Polygon-->>Backend: Transaction found/not found
    Backend-->>Frontend: Verification result + proof
    Frontend-->>Recruiter: Show verification status ✅ or ❌
```

### Blockchain Storage Method

CredSure stores credential hashes in the **transaction data field** of Polygon transactions:

```javascript
// Format: CREDSURE:hash:slug
data: ethers.toUtf8Bytes(`CREDSURE:${credentialHash}:${slug}`)
```

This approach:
- ✅ Doesn't require smart contract deployment
- ✅ Low gas fees (~$0.001 per transaction)
- ✅ Immutable and tamper-proof
- ✅ Publicly verifiable on blockchain explorers

---

## 📚 API Documentation

### Base URL
```
Production: https://api.siddz.com/credsure
Development: http://localhost:3001
```

### Authentication

All authenticated routes require a JWT token in the Authorization header:
```
Authorization: Bearer <token>
```

### Endpoints

#### Student Authentication

**Register Student**
```http
POST /api/student/register
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword",
  "rollNumber": "2021CS001"
}

Response: { "token": "jwt_token", "student": {...} }
```

**Login Student**
```http
POST /api/student/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "securepassword"
}

Response: { "token": "jwt_token", "student": {...} }
```

**Verify Token**
```http
POST /api/student/verify
Content-Type: application/json

{
  "token": "jwt_token"
}

Response: { "valid": true, "student": {...} }
```

#### University Authentication

**Register University**
```http
POST /api/university/register
Content-Type: application/json

{
  "name": "Stanford University",
  "email": "admin@stanford.edu",
  "password": "securepassword"
}

Response: { "token": "jwt_token", "university": {...} }
```

**Login University**
```http
POST /api/university/login
Content-Type: application/json

{
  "email": "admin@stanford.edu",
  "password": "securepassword"
}

Response: { "token": "jwt_token", "university": {...} }
```

#### Credentials

**Issue Credential**
```http
POST /api/credentials/issue
Authorization: Bearer <university_token>
Content-Type: multipart/form-data

Fields:
- studentEmail: string
- credentialType: string
- file: File (PDF/Image)

Response: {
  "message": "Credential issued successfully",
  "credential": {...},
  "transactionHash": "0x..."
}
```

**Get Student Credentials**
```http
GET /api/credentials/student
Authorization: Bearer <student_token>

Response: [
  {
    "id": "...",
    "credentialType": "Degree",
    "university": {...},
    "slug": "abc123",
    "fileUrl": "...",
    "blockchainHash": "0x...",
    "issuedAt": "..."
  }
]
```

**Verify Credential**
```http
GET /api/credentials/verify/:slug

Response: {
  "valid": true,
  "credential": {...},
  "blockchainVerified": true,
  "transactionHash": "0x..."
}
```

**Get University Issued Credentials**
```http
GET /api/credentials/university
Authorization: Bearer <university_token>

Response: [...]
```

---

## 🌐 Deployment

### Frontend (Vercel)

1. **Push to GitHub**
2. **Connect to Vercel**
   - Import repository
   - Framework: Next.js
   - Build command: `npm run build`
   - Output directory: `.next`
3. **Add Environment Variables**
   - Update `config.json` with production URLs
4. **Deploy** 🚀

### Backend (VPS/Cloud)

1. **Setup server** (Ubuntu recommended)
   ```bash
   sudo apt update
   sudo apt install nodejs npm nginx
   ```

2. **Clone and install**
   ```bash
   git clone <repo>
   cd Backend
   npm install
   ```

3. **Configure environment**
   ```bash
   nano .env
   # Add production environment variables
   ```

4. **Setup PM2** (process manager)
   ```bash
   sudo npm install -g pm2
   pm2 start server.js --name credsure-backend
   pm2 startup
   pm2 save
   ```

5. **Configure Nginx** (reverse proxy)
   ```nginx
   server {
       listen 80;
       server_name api.yourdomain.com;
       
       location / {
           proxy_pass http://localhost:3001;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

6. **SSL Certificate**
   ```bash
   sudo apt install certbot python3-certbot-nginx
   sudo certbot --nginx -d api.yourdomain.com
   ```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/AmazingFeature
   ```
5. **Open a Pull Request**

### Development Guidelines

- Follow the existing code style
- Write meaningful commit messages
- Add comments for complex logic
- Test your changes thoroughly
- Update documentation if needed

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- **Polygon** for providing a fast and affordable blockchain infrastructure
- **Next.js** team for an amazing React framework
- **Hono.js** for a lightweight and fast backend framework
- **Radix UI** for accessible component primitives
- **Tailwind CSS** for utility-first styling
- All open-source contributors who made this possible

---

## 📞 Contact

**Developer**: Siddharth  
**Project Link**: [https://credsure.siddz.com](https://credsure.siddz.com)  
**GitHub**: [https://github.com/SiddDevZ/credsure-hackathon](https://github.com/SiddDevZ/credsure-hackathon)

---

## 🎯 Future Roadmap

- [ ] Implement smart contracts for credential registry
- [ ] Add support for multiple blockchain networks
- [ ] Integrate IPFS for decentralized file storage
- [ ] Add credential templates for different certificate types
- [ ] Implement batch credential issuance
- [ ] Add analytics dashboard for universities
- [ ] Support for NFT-based credentials
- [ ] Mobile app (React Native)
- [ ] Integration with LinkedIn and other platforms
- [ ] Multi-language support
- [ ] Advanced permission management

---

<div align="center">

**Built with ❤️ by Siddharth**

⭐ Star this repo if you find it helpful!

</div>
