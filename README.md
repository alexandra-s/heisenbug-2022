Additional materials for my talk at Heisenbug 2022

# Getting started

## MobSF

```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

MobSF web interface is now available at http://localhost:8000/

## Drozer

### 1. Install Drozer Agent 

get it from https://github.com/FSecureLABS/drozer/releases/download/2.3.4/drozer-agent-2.3.4.apk

```
adb install drozer-agent-2.3.4.apk
```

### 2. Run Agent

Run app. Tap on Embedded Server, enable the server

### 3. Troubleshoot Agent

If the app says

> Attempting to bind to port 31415...
> IO Error. Resetting connection.

Try to change the port used by the embedded server:
Settings > Embedded Server > Port
set to `60000`
Save settings, restart the server

### 4. Run console
#### If Agent uses default port (31415)
```
docker run -it fsecurelabs/drozer

drozer console connect --server <phone IP address>
```

#### If Agent uses custom port (60000)
```
adb forward tcp:31415 tcp:60000

docker run -it --add-host host.docker.internal:host-gateway fsecurelabs/drozer

drozer console connect --server host.docker.internal
```

