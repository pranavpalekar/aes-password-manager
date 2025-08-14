# AES Password Manager - Project Documentation

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [System Architecture](#2-system-architecture)
3. [Core Components](#3-core-components)
4. [Security Implementation](#4-security-implementation)
5. [User Flow](#5-user-flow)
6. [Technical Implementation Details](#6-technical-implementation-details)
7. [Future Enhancements](#7-future-enhancements)
8. [Core Functionality and Implementation](#8-core-functionality-and-implementation)
9. [How It Works](#9-how-it-works)
10. [Key Features and Benefits](#10-key-features-and-benefits)

## 1. Project Overview
The AES Password Manager is a sophisticated blockchain-based password management solution that combines the security of blockchain technology with the convenience of modern web applications. This project demonstrates the implementation of a secure, decentralized password management system that allows users to store, manage, and synchronize their passwords across multiple devices.

## 2. System Architecture

### 2.1 High-Level Architecture
The system is built using a multi-tier architecture:
- **Smart Contract Layer**: Handles secure storage and device management
- **Backend Layer**: Manages API endpoints and data processing
- **Frontend Layer**: Provides user interface and interaction
- **Extension Layer**: Enables browser integration

### 2.2 Technology Stack
- **Blockchain**: Ethereum (using Hardhat development environment)
- **Smart Contracts**: Solidity
- **Backend**: Node.js with Express
- **Frontend**: React with Tailwind CSS
- **Development Tools**: Hardhat, Web3.js

## 3. Core Components

### 3.1 Smart Contract (VaultManager.sol)
The smart contract serves as the foundation of the system's security and functionality.

#### Key Features:
1. **Vault Management**
   - Secure storage of user vault data using Content Identifiers (CIDs)
   - Encrypted storage of sensitive information
   - Unique vault for each user

2. **Device Management**
   - Multi-device support
   - Device registration and authentication
   - Synchronization across devices

3. **Security Features**
   - Address-based access control
   - Event logging for audit trails
   - Timestamp tracking for synchronization

#### Main Functions:
```solidity
- setVaultCID(string memory cid)
- getVaultCID(address user)
- addDevice(string memory deviceId, string memory deviceName)
- removeDevice(string memory deviceId)
- getDevices(address user)
- isDeviceRegistered(address user, string memory deviceId)
```

### 3.2 Backend Server
The Express.js server provides the necessary API endpoints for the frontend and extension to interact with the system.

#### Key Features:
1. **API Endpoints**
   - Health check endpoint
   - Password management endpoints
   - Device synchronization endpoints

2. **Data Management**
   - Local storage integration
   - Blockchain interaction
   - Data validation and sanitization

3. **Security Measures**
   - CORS implementation
   - Input validation
   - Error handling

### 3.3 Frontend Application
The web interface provides users with an intuitive way to manage their passwords.

#### Key Features:
1. **User Interface**
   - Modern, responsive design
   - Tailwind CSS styling
   - Intuitive navigation

2. **Functionality**
   - Password management
   - Device synchronization
   - Security settings

3. **Integration**
   - Blockchain wallet connection
   - API integration
   - Extension support

## 4. Security Implementation

### 4.1 Blockchain Security
- Smart contract security measures
- Access control mechanisms
- Event logging for audit trails

### 4.2 Data Security
- Encryption of sensitive data
- Secure storage mechanisms
- Multi-device synchronization security

### 4.3 Access Control
- Device-based authentication
- User address verification
- Synchronization controls

## 5. User Flow

1. **Initial Setup**
   - User connects their wallet
   - Initial device registration
   - Vault creation

2. **Password Management**
   - Adding new passwords
   - Viewing stored passwords
   - Updating existing passwords
   - Deleting passwords

3. **Device Synchronization**
   - Adding new devices
   - Synchronizing data across devices
   - Managing device access

## 6. Technical Implementation Details

### 6.1 Smart Contract Implementation
The VaultManager contract uses several key data structures:
```solidity
mapping(address => string) private userVaultCIDs;
mapping(address => mapping(string => bool)) public userDevices;
mapping(address => string[]) public userDeviceList;
mapping(address => uint256) public lastSyncTime;
```

### 6.2 Backend Implementation
The server implements RESTful API endpoints with proper error handling and data validation:
```javascript
- GET /api/check
- GET /api/passwords
- POST /api/passwords
```

### 6.3 Frontend Implementation
The frontend uses modern React practices with Tailwind CSS for styling and Web3.js for blockchain interaction.

## 7. Future Enhancements

1. **Additional Security Features**
   - Two-factor authentication
   - Biometric authentication
   - Advanced encryption methods

2. **User Experience Improvements**
   - Enhanced UI/UX
   - Mobile application
   - Offline support

3. **Technical Improvements**
   - Gas optimization
   - Enhanced synchronization
   - Advanced backup features

## 8. Core Functionality and Implementation

### 8.1 Basic Working Principle
The project is a blockchain-based password manager that allows users to:
1. Securely store their passwords
2. Access passwords across multiple devices
3. Manage their passwords through a user-friendly interface
4. Synchronize data across devices securely

## 9. How It Works

### 9.1 User Registration and Setup
1. **Initial Connection**
   - User connects their Ethereum wallet to the application
   - System creates a unique vault for the user on the blockchain
   - First device is registered automatically

2. **Vault Creation**
   - A unique Content Identifier (CID) is generated for the user's vault
   - This CID is stored on the blockchain through the VaultManager contract
   - The actual password data is encrypted and stored securely

### 9.2 Password Management

#### Adding Passwords
1. User enters website credentials (username, password, website)
2. System encrypts the data
3. Data is stored in the user's vault
4. Changes are synchronized to the blockchain

#### Accessing Passwords
1. User authenticates with their wallet
2. System retrieves the vault CID from the blockchain
3. Decrypts and displays the stored passwords
4. Provides secure access to the credentials

### 9.3 Multi-Device Synchronization

1. **Device Registration**
   ```solidity
   function addDevice(string memory deviceId, string memory deviceName) public {
       require(!userDevices[msg.sender][deviceId], "Device already registered");
       userDevices[msg.sender][deviceId] = true;
       userDeviceList[msg.sender].push(deviceId);
       emit DeviceAdded(msg.sender, deviceId, deviceName);
   }
   ```

2. **Synchronization Process**
   - Each device maintains a local copy of the vault
   - Changes are pushed to the blockchain
   - Other devices pull updates from the blockchain
   - Timestamps ensure proper synchronization

## 10. Key Features and Benefits

1. **Security**
   - Blockchain-based storage
   - Encryption at rest
   - Multi-device security

2. **Convenience**
   - Cross-device synchronization
   - Easy password management
   - User-friendly interface

3. **Reliability**
   - Decentralized storage
   - Backup capabilities
   - Data consistency

---

This documentation provides a comprehensive overview of the AES Password Manager project, its architecture, implementation details, and functionality. For more detailed information about specific components or features, please refer to the respective sections above. 