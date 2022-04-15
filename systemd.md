### List all timers
```bash
systemctl list-timers --all
```

### Start service
```bash
systemctl start your_service.service
```

### See all service logs
```bash
journalctl -fu your_service.service
```

### Check all services for state:
```bash
systemctl list-units --state enabled|failed
```
