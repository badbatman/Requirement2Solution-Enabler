Title: Funds Transfer Authorization
Entities: Customer, MobileApp, AuthService, FraudDetector, CoreBanking

Input/Output Requirements:
| AC Ref | Type  | Field         | Requirement          | Constraints        | Security        |
|--------|-------|---------------|----------------------|--------------------|-----------------|
| AC1    | Input | Amount        | Numeric validation   | >0, <50,000 USD    | -               |
| AC2    | Input | BiometricData | Encryption           | ISO/IEC 19794-2    | AES-GCM-256     |
| AC3    | Output| AuthResult    | Machine-readable     | JSON schema v4     | Digital signing |

AC1: GIVEN Transfer request 
     WHEN amount exceeds $10,000 
     THEN require manager approval

AC2: GIVEN New device login
     WHEN initiating transfer
     THEN enforce biometric auth

AC3: GIVEN Fraud score >75
     WHEN any transaction
     THEN block and alert security
