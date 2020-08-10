# Kill process running on port {port number} in MacOS

### Get the PID
```
sudo lsof -i tcp:{port number}
```

### Kill
```
kill -9 {PID}
```

### 한방에 kill
```
kill $(lsof -t -i:{port number})
```
