# UFW Firewall Configuration

## Objective

Configure a basic firewall using UFW.

## What is a Firewall?

A firewall monitors and controls incoming and outgoing network traffic based on predefined security rules. It helps protect the system from unauthorized access.

## Rules Configured

1. Allow SSH (Port 22)
   - Enables secure remote administration.

2. Deny HTTP (Port 80)
   - Blocks unencrypted web traffic.

3. Allow HTTPS (Port 443)
   - Allows secure encrypted web traffic.

4. Deny Telnet (Port 23)
   - Blocks the insecure Telnet service.

## Verification

Firewall status was checked using:

sudo ufw status verbose

## Testing

HTTP traffic on port 80 was denied.
SSH and HTTPS remained allowed.

