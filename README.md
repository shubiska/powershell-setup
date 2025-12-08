# Shubiska Powershell Setup

# Install Git & Zen Browser 

```
$gitUrl = "https://github.com/git-for-windows/git/releases/latest/download/Git-64-bit.exe"
$gitInstaller = "$env:TEMP\git_installer.exe"

Invoke-WebRequest -Uri $gitUrl -OutFile $gitInstaller
Start-Process $gitInstaller -ArgumentList "/VERYSILENT /NORESTART" -Wait
Remove-Item $gitInstaller

# === Install Zen Browser ===
$zenUrl = "https://github.com/zen-browser/desktop/releases/latest/download/zen.installer.exe"
$zenInstaller = "$env:TEMP\zen_installer.exe"

Invoke-WebRequest -Uri $zenUrl -OutFile $zenInstaller
Start-Process $zenInstaller -ArgumentList "/S" -Wait
Remove-Item $zenInstaller
```

# Links
    Windows SDK: https://go.microsoft.com/fwlink/?linkid=2342616
    VSCodium: https://github.com/VSCodium/vscodium/releases
    LLVM: https://github.com/llvm/llvm-project/releases
    
# Add LLVM to PATH

```
$Path = "C:\Program Files\LLVM\bin"

if (-not (Test-Path $Path)) {
    Write-Host "LLVM IS NOT INSTALLED."
    exit 1
}

$OldPath = [Environment]::GetEnvironmentVariable("PATH", "User")

if ($OldPath -split ';' -contains $Path) {
    Write-Host "LLVM ALREADY IN PATH."
    exit 0
}

$NewPath = $OldPath + ";" + $Path
[Environment]::SetEnvironmentVariable("PATH", $NewPath, "User")
Write-Host "LLVM ADDED TO PATH"
```

# Defender Remover
## This last part is not recommended, unsafe, and could damage your Windows installation.
## If you decide to run this, do it at your own risk.
## Don't run this if you don't know what you are doing!
## Disable Windows Defender before continuing.

```
$Path = "$env:TEMP\defender-remover"
git clone https://github.com/ionuttbara/windows-defender-remover.git $Path
cd $Path

./Script_Run.bat
```
