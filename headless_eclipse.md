### Start eclipse in headless mode for Linux:

#### When Xvbf instanse is not started yet
```bash
Xvfb :1 -screen 0 1024x768x24 & DISPLAY=:1 $ECLIPSE_HOME/eclimd -b
```


#### When Xvbf instance already started
```bash
DISPLAY=:1 $ECLIPSE_HOME/eclimd -b
```
