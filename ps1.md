### Net Con mon
```
while ($true) {
    Get-Process ms-teams | ForEach-Object {
        $id = $_.Id
        Write-Host "`nConnections for MS Teams process $id" -ForegroundColor Green
        Get-NetTCPConnection | Where-Object { $_.OwningProcess -eq $id } |
        Select-Object LocalAddress, LocalPort, RemoteAddress, RemotePort, State
    }
    Start-Sleep -Seconds 2
}
```
### Telnet
```
[CmdletBinding()]
Param(
  [Parameter(Mandatory=$True,Position=1)]
   [string]$ip,
    
   [Parameter(Mandatory=$True,Position=2)]
   [int]$port
)

$connection = New-Object System.Net.Sockets.TcpClient($ip, $port)
if ($connection.Connected) {
    Return "Connection Success"
}
else {
    Return "Connection Failed"
}
```
