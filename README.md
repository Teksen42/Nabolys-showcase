<div align="center">

  <img src="https://capsule-render.vercel.app/api?type=waving&height=180&color=0:111111,100:E8590C&text=Nabolys&fontAlign=50&fontAlignY=36&fontColor=FFFFFF&fontSize=60&desc=Emergency%20preparedness%20that%20works%20without%20the%20network&descAlign=50&descAlignY=60&descSize=18" alt="Nabolys banner" width="100%" />

  <img src="https://img.shields.io/badge/Own%20project-Yasir%20Lokman%20Teksen-111111?style=for-the-badge" alt="Own project" />
  <img src="https://img.shields.io/badge/Platform-Android%20%C2%B7%20iPhone-E8590C?style=for-the-badge" alt="Android and iPhone" />
  <img src="https://img.shields.io/badge/Status-in%20development-E5A000?style=for-the-badge" alt="In development" />

</div>

> This repository shows the project. The source code is not public. Read more about the app on its website: [nabolys.azurewebsites.net](https://nabolys.azurewebsites.net/).

## What it is

Nabolys ("the neighbours' light") is a Danish app for **Android and iPhone** that helps a family and their neighbours get ready for a crisis and keep in touch when the mobile network or the power is gone.

- **Stock** with best-before dates, and a warning before things expire.
- **A three-day list** worked out for the people who live there (adults, children, small children and pets), based on the Danish authorities' advice.
- **A family plan**: where to meet, who to call and who does what.
- **"I'm ok" check-in** and family messages.
- **Emergency screen**: a dark screen with big buttons, the plan and the latest check-ins.
- **Walkie-talkie**: hold the button and talk to the family near you, phone to phone.
- **Neighbourhoods** (on its way): a closed group for your building or street, where neighbours write to each other.

Nabolys is a private project, not an official app, and it does not replace 112 or official warnings.

## Works without the network

When the network is down, phones near each other can send check-ins, messages and voice over **Bluetooth Low Energy**, also between iPhone and Android, and they are passed on to the server when there is a network again. Everything a family shares is **end-to-end encrypted**, so the server cannot read it. Data on the phone is stored in an encrypted database.

## Status

The MVP is built, and the app is on its way to the App Store and Google Play. Security-related parts get a written internal security review, and every change runs through automated tests and CI. The server and the website run on Azure.

## Screenshots

<p align="center">
  <img src="images/nabolys.webp" alt="Nabolys: the home screen, the stock list and the three-day list" width="100%" />
  <br />
  <em>Home, stock and the three-day list</em>
</p>

<p align="center">
  <img src="images/nabolys-krise.webp" alt="Nabolys: the family check-in, the dark emergency screen and the walkie-talkie" width="100%" />
  <br />
  <em>Family check-in, the dark emergency screen and the walkie-talkie</em>
</p>

## Stack

<p>
  <img src="https://img.shields.io/badge/C%23-512BD4?style=flat-square&logo=dotnet&logoColor=white" alt="C#" />
  <img src="https://img.shields.io/badge/.NET%2010%20%2F%20ASP.NET%20Core-512BD4?style=flat-square&logo=dotnet&logoColor=white" alt=".NET 10 and ASP.NET Core" />
  <img src="https://img.shields.io/badge/SignalR-512BD4?style=flat-square" alt="SignalR" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/React%20Native-20232A?style=flat-square&logo=react&logoColor=61DAFB" alt="React Native" />
  <img src="https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white" alt="Expo" />
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white" alt="Kotlin" />
  <img src="https://img.shields.io/badge/Swift-F05138?style=flat-square&logo=swift&logoColor=white" alt="Swift" />
  <img src="https://img.shields.io/badge/Bluetooth%20LE-0082FC?style=flat-square&logo=bluetooth&logoColor=white" alt="Bluetooth LE" />
  <img src="https://img.shields.io/badge/SQL%20Server%20%2F%20Azure%20SQL-CC2927?style=flat-square" alt="SQL Server and Azure SQL" />
  <img src="https://img.shields.io/badge/SQLite%20%2F%20SQLCipher-003B57?style=flat-square&logo=sqlite&logoColor=white" alt="SQLite and SQLCipher" />
  <img src="https://img.shields.io/badge/Azure%20App%20Service-0078D4?style=flat-square" alt="Azure App Service" />
  <img src="https://img.shields.io/badge/Azure%20Key%20Vault-0078D4?style=flat-square" alt="Azure Key Vault" />
  <img src="https://img.shields.io/badge/Entra%20ID-0078D4?style=flat-square" alt="Entra ID" />
  <img src="https://img.shields.io/badge/Bicep-0078D4?style=flat-square" alt="Bicep" />
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white" alt="GitHub Actions" />
</p>

| Part | What it uses |
|---|---|
| **App** (Android, iPhone and web) | React Native with Expo (SDK 58), written in TypeScript. One codebase gives Android, iPhone and a web version. SQLCipher (via expo-sqlite) for the encrypted database on the phone, with the key in the phone's secure storage (expo-secure-store). The camera reads barcodes and QR codes. |
| **Encryption** (`packages/core`) | TypeScript with the @noble libraries: XChaCha20-Poly1305 to encrypt messages, Ed25519 for signatures, HPKE to share keys, and SHA-256. End-to-end encrypted, so the server cannot read the messages. |
| **Bluetooth without the network** | Kotlin on Android, as an Expo module using Bluetooth Low Energy. Swift on iPhone, built and tested in CI. |
| **Server** | C# with ASP.NET Core 10 and Entity Framework Core 10. SQL Server (LocalDB in development, Azure SQL in production). SignalR for real-time messages and online status. Azure Communication Services sends login codes by e-mail. |
| **Operations and tests** | Azure (App Service, Azure SQL, Key Vault and Application Insights), set up with Bicep, and deploys that sign in through Entra ID. GitHub Actions for CI: tests, a scan for leaked secrets (gitleaks) and deploy. EAS Build builds the phone apps in the cloud. |

---

Made by [Yasir Lokman Teksen](https://github.com/Teksen42). More about me on [teksen42.github.io](https://teksen42.github.io).
