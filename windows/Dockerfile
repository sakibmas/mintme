FROM mcr.microsoft.com/windows/servercore:ltsc2019
SHELL ["powershell","-command"]
RUN Start-BitsTransfer -Source https://github.com/mintme-com/miner/releases/download/v2.8.0/webchain-miner-2.8.0-win64.zip
RUN Expand-Archive -LiteralPath webchain-miner-2.8.0-win64.zip
RUN Remove-Item webchain-miner-2.8.0-win64.zip
WORKDIR /webchain-miner-2.8.0-win64
RUN copy-item config.json configV1.json
RUN (Get-Content -path configV1.json) -replace 'YOUR_WALLET','0x4499d5d662caf6e87dd5ce283441e001ce3ca825' | Add-Content configV2.json
RUN (Get-Content -path configV2.json) -replace '0\",','0x17\",' | Add-Content configV3.json
RUN (Get-Content -path configV3.json) -replace '75,','80,' | Add-Content configV4.json
RUN (Get-Content -path configV4.json) -replace '5,','1,' | Add-Content configV5.json
SHELL ["cmd.exe","/C"]
ENTRYPOINT ["webchain-miner.exe","--config=configV5.json"]
