# Shubiska Powershell Setup

# Install Git & Zen Browser 

function WebInstall {
    param(
        [string]$Url,
        [string]$SilentArgs
    )

    $Installer = "$env:TEMP\installer.exe"

    Invoke-WebRequest -Uri $Url -OutFile $Installer
    Start-Process $Installer -ArgumentList $SilentArgs -Wait
    Remove-Item $Installer
}

WebInstall "https://github.com/git-for-windows/git/releases/latest/download/Git-64-bit.exe" "/VERYSILENT /NORESTART"
WebInstall "https://github.com/zen-browser/desktop/releases/latest/download/zen.installer.exe" "/S"

# Links
    Windows SDK: https://go.microsoft.com/fwlink/?linkid=2342616
    VSCodium: https://github.com/VSCodium/vscodium/releases
    LLVM: https://github.com/llvm/llvm-project/releases
    
# Add LLVM to PATH

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

* This last part is not recommended, unsafe, and could damage your Windows installation.
* If you decide to run this, do it at your own risk.
* Don't run this if you don't know what you are doing!
* Disable Windows Defender before continuing.
# Defender Remover

$Path = "$env:TEMP\defender-remover"
git clone https://github.com/ionuttbara/windows-defender-remover.git $Path
cd $Path

./Script_Run.bat
