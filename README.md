# STX-Disaster-Relief Donation Smart Contract

## Overview
This smart contract provides a transparent and secure way to manage disaster-relief donations. It enables users to donate funds, allows administrators to manage recipients and settings, and permits approved recipients to withdraw allocated funds.

## Features
- **Donations**: Users can donate within predefined limits.
- **Recipient Management**: Administrators can add, remove, and update recipients and their allocations.
- **Withdrawals**: Recipients can withdraw allocated funds with a cooldown period.
- **Administrative Controls**: The contract supports pausing operations, setting donation limits, and emergency shutdown.
- **Refund Requests**: Donors can request refunds within a limited time frame.
- **Audit Logging**: Records key actions for transparency.

## Constants
- `ERR_UNAUTHORIZED (u1)`: Unauthorized action attempt.
- `ERR_INVALID_AMOUNT (u2)`: Invalid amount provided.
- `ERR_INSUFFICIENT_FUNDS (u3)`: Not enough funds available.
- `ERR_RECIPIENT_NOT_FOUND (u4)`: Recipient does not exist.
- `ERR_RECIPIENT_EXISTS (u5)`: Recipient already exists.
- `ERR_NOT_CONFIRMED (u8)`: Confirmation required.
- `ERR_UNCHANGED_STATE (u9)`: No state change detected.
- `withdrawal-cooldown (u86400)`: 24-hour waiting period between withdrawals.

## Data Storage
- `total-funds`: Tracks total contract funds.
- `admin`: Stores the contract administrator.
- `min-donation` / `max-donation`: Defines donation range.
- `paused`: Boolean indicating contract activity status.
- `donations`: Maps donors to their total donation amount.
- `recipients`: Stores recipients and their fund allocations.
- `last-withdrawal`: Maps recipients to their last withdrawal timestamp.

## Public Functions

### Donations
- **`(donate amount)`**: Allows users to donate funds within limits.
- **`(request-refund amount)`**: Enables donors to request refunds within the cooldown period.

### Recipient Management
- **`(add-recipient recipient allocation)`**: Admins add a recipient with a specific allocation.
- **`(update-recipient-allocation recipient new-allocation)`**: Admins update a recipient's fund allocation.
- **`(remove-recipient recipient)`**: Admins remove a recipient.
- **`(confirm-remove-recipient recipient confirm)`**: Confirms recipient removal.

### Withdrawals
- **`(withdraw amount)`**: Allows recipients to withdraw allocated funds within limits and cooldown period.

### Administrative Functions
- **`(set-admin new-admin)`**: Transfers admin privileges.
- **`(set-donation-limits new-min new-max)`**: Updates min/max donation limits.
- **`(set-paused new-paused-state)`**: Toggles contract pause state.
- **`(emergency-shutdown)`**: Pauses the contract in emergencies.
- **`(log-audit action-type actor)`**: Records audit logs.

### Read-Only Functions
- **`(get-donation user)`**: Returns the total donation of a user.
- **`(get-total-funds)`**: Retrieves total contract funds.
- **`(is-paused)`**: Checks if the contract is paused.
- **`(get-recipient-allocation recipient)`**: Returns a recipient’s allocation.
- **`(get-admin)`**: Retrieves the current admin.
- **`(get-user-history user)`**: Provides donation and withdrawal history for a user.

## Security Considerations
- Only the admin can modify recipients and contract settings.
- The contract includes cooldown periods to prevent fund abuse.
- Emergency shutdown allows quick response to security threats.

