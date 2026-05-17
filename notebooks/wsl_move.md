# Moving WSL to D Drive

## Step 1: Install WSL Normally (If you haven't already)

WSL itself (the architecture) must reside on your main Windows system drive, but the massive Linux filesystems (the virtual disks) can live on your external drive.

1. Open **PowerShell** or **Command Prompt** as **Administrator**.
2. Run the install command:
```powershell
wsl --install

```


3. Restart your computer if prompted, and set up your initial Linux username and password.

---

## Step 2: Export your Distro to a File

We will take a snapshot of your current Linux installation and save it as a `.tar` file.

1. Make sure your WSL distro is completely shut down:
```powershell
wsl --shutdown

```


2. Create a temporary folder on your external drive (e.g., `D:\WSL_Backup`).
3. Export the distro (assuming you are using `Ubuntu`, replace if using a different one):

```powershell
   wsl --export Ubuntu D:\WSL_Backup\ubuntu-backup.tar

```

## Step 3: Unregister the C: Drive Version

Before importing it to the new location, you need to remove the old instance from your C: drive to avoid naming conflicts.

> ⚠️ **Warning:** This will delete all data inside the C: drive instance of that specific distro. Ensure your `.tar` file export in Step 2 was successful before running this.

```powershell
wsl --unregister Ubuntu

```

---

## Step 4: Import Distro to your External Drive

Now, you will target the external drive as the final home for your Linux installation.

1. Create a permanent directory on your external drive where the active virtual disk will live (e.g., `D:\WSL\Ubuntu`).
2. Import the `.tar` file into that directory:

```powershell
   wsl --import Ubuntu D:\WSL\Ubuntu D:\WSL_Backup\ubuntu-backup.tar

```

*(Syntax: `wsl --import [DistroName] [InstallLocation] [PathToTarFile]`)*

You can now delete the temporary `ubuntu-backup.tar` file to free up space.

---

## Install GCP SDK

Please note that if WSL is installed in D drive, we cannot use snap to install GCP CLI

```bash
sudo apt-get update
```

```bash
sudo apt-get install ca-certificates gnupg curl
```

```bash
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo gpg --dearmor -o /usr/share/keyrings/cloud.google.gpg
```

```bash
echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
```

```bash
sudo apt-get update && sudo apt-get install google-cloud-cli
```


Please refer to the official installation guide for the latest: https://docs.cloud.google.com/sdk/docs/install-sdk#deb


