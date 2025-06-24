To hide usernames on the Windows login and lock screens using **PowerShell**, run the following commands as an **Administrator**.  

---

## **1. Hide Last Logged-in Username (Login Screen)**
This prevents Windows from displaying the last logged-in user at the sign-in screen.

### **PowerShell Command:**
```powershell
New-ItemProperty -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\System" -Name "dontdisplaylastusername" -Value 1 -PropertyType DWord -Force
```

---

## **2. Hide Username When the Screen is Locked**
This ensures that the lock screen does not show the current user’s details.

### **PowerShell Command:**
```powershell
New-ItemProperty -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\System" -Name "dontdisplaylockeduserid" -Value 3 -PropertyType DWord -Force
```
- `3` = Do not display user information.  
- Other values:
  - `1` = Show full name
  - `2` = Show username only

---

## **3. Disable Username Display at Sign-in**
Prevents usernames from appearing at sign-in.

### **PowerShell Command:**
```powershell
New-ItemProperty -Path "HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\System" -Name "DontDisplayUserName" -Value 1 -PropertyType DWord -Force
```

---

## **4. Apply Changes Immediately**
To apply these changes without rebooting, restart the Windows Explorer process:

### **PowerShell Command:**
```powershell
Stop-Process -Name explorer -Force; Start-Process explorer
```
Or, restart the system for full effect:
```powershell
shutdown /r /t 0
```

---

### **Verification**
After applying these settings:
1. **Lock your screen** (`Win + L`) – Ensure no username is displayed.
2. **Sign out** – The login screen should not show the last logged-in user.

✅ These commands **harden Windows against username enumeration** by social engineering or physical access attacks.
