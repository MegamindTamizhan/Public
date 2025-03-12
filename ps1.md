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
### 
```

```
