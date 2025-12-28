# 🏦 Solana Token Vesting Smart Contract (Anchor)

A fully on-chain token vesting system built on Solana using Anchor that allows companies to create vesting schedules for employees, enforce cliff periods, and enable linear token unlock with secure PDA-based treasury control.

---

## 🚀 Features

- Create company-level vesting vaults (treasury)
- Create employee-specific vesting schedules
- Supports cliff period + linear vesting
- Secure PDA-controlled treasury vault
- Prevents early claims before cliff
- Prevents over-withdrawals
- Fully SPL Token 2022 compatible via token_interface
- Uses Associated Token Accounts (ATA)

---

## 🧠 How It Works

### 1️⃣ Company Creates Vesting Treasury
A company creates a vesting account linked to a mint and a PDA-owned treasury vault that stores the vesting tokens.

### 2️⃣ Create Employee Vesting
For each employee, a vesting account is created containing:
- Start time
- End time
- Cliff time
- Total allocated tokens

### 3️⃣ Claim Tokens
Employees can claim vested tokens:
- Only after cliff
- Linearly unlocked over time
- Cannot withdraw more than allocated

Treasury PDA securely signs all token transfers.

---

## 📦 Program Accounts

| Account | Purpose |
|--------|--------|
| VestingAccount | Stores company vesting info |
| EmployeeAccount | Stores employee vesting schedule |
| treasury_token_account | PDA-owned token vault |
| employee_token_account | Employee ATA to receive tokens |

---

## 🗂 PDA Structure

| PDA | Seeds |
|----|-----|
| Vesting Account | [company_name] |
| Treasury Vault | ["vesting_treasury", company_name] |
| Employee Vesting | ["employee_vesting", beneficiary, vesting_account] |

---

## 🛠 Instructions

### create_vesting_account(company_name)
Creates company vesting PDA and treasury token vault.

### create_employee_vesting(start_time, end_time, total_amount, cliff_time)
Creates vesting schedule for an employee.

### claim_tokens(company_name)
Allows employee to claim unlocked tokens.

---

## ⏳ Vesting Formula

