### 🔹 Secure Remote Access with OpenSSH (with MFA)

  - Installed and configured an OpenSSH server on Ubuntu for secure remote access.
  
  - Implemented key-based authentication and integrated Google Authenticator MFA for an additional security layer.
  Steps included:
  
  1. Installed the PAM module for Google Authenticator:
  ```
  sudo apt install libpam-google-authenticator
  ```
  
  2. Enabled MFA per user:
  ```
  google-authenticator
  ```
  
  3. Updated the PAM config at /etc/pam.d/sshd:
  ```
  auth required pam_google_authenticator.so
  ```
  
  4. Edited /etc/ssh/sshd_config to allow both public key and MFA:
  ```
  ChallengeResponseAuthentication yes
  AuthenticationMethods publickey,keyboard-interactive
  ```
  
  5. Restarted SSH and tested login using a one-time MFA code.
  
  Monitored /var/log/auth.log for failed logins, brute-force attempts, and MFA validation.
  Restricted SSH access to specific IP ranges for better control.
