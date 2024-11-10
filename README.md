# forza-udp-databroker-proxy
In inspiration from https://github.com/fabiomix here is a small modification to gather data from Forza Telemetry over UPD stream to feed into the Kuksa.val databroker with python sdk.

# Getting started:
## Forza settings
Enable data-out feature in game settings, pointing to the host that runs docker, port `9999`

Settings -> GHUD and Gameplay -> (last settings of the long list) 

Dataoutput=ON, IP=<IP adress of recieving PC/RaspberryPI>, PORT=9999

See details: [Forza Motorsport 7 'Data Out' feature details](https://forums.forzamotorsport.net/turn10_postst128499_Forza-Motorsport-7--Data-Out--feature-details.aspx)
## Install docker.io / podman / etc. 
## Run kuksa.val databoker: 
```console
docker run -it --rm --name Server --network host ghcr.io/eclipse-kuksa/kuksa-databroker:main --insecure
```
## Install kuksa.val python sdk: 
```console
pip install kuksa-client
```
or use venv:
```console
python -m venv my-venv
my-venv/bin/pip install
```
## Run script
```console
python3 ForzaUdpDatabroker-proxy.py
```
or
```console
my-venv/bin/python3 ForzaUdpDatabroker-proxy.py
```
## Check results with databroker client
Run databroker client
```console
docker run -it --rm --net=host ghcr.io/eclipse-kuksa/kuksa-python-sdk/kuksa-client:main
subscribe Vehicle.Body.Lights.Brake.IsActive
```
See the output when pressing the Brake in Forza
