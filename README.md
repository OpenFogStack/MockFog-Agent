# MockFog-Agent

This project is part of MockFog which includes the following subprojects:
* [MockFog-Meta](https://github.com/OpenFogStack/MockFog-Meta) Meta repository with a presentation and a demo video
* [MockFog-IaC](https://github.com/OpenFogStack/MockFog-IaC) MockFog Infrastructure as Code artifacts
* [MockFog-NodeManager](https://github.com/OpenFogStack/MockFog-NodeManager) MockFog Node Manager
* [MockFog-Agent](https://github.com/OpenFogStack/MockFog-Agent) MockFog Agent
* [MockFogLight](https://github.com/OpenFogStack/MockFogLight) A lightweight version of MockFog without a visual interface

Fog computing is an emerging computing paradigm that uses processing and storage capabilities located at the edge, in the cloud, and possibly in between. Testing fog applications, however, is hard since runtime infrastructures will typically be in use or may not exist, yet.
MockFog is a tool that can be used to emulate such infrastructures in the cloud. Developers can freely design emulated fog infrastructures, configure their performance characteristics, and inject failures at runtime to evaluate their application in various deployments and failure scenarios.

If you use this software in a publication, please cite it as:

### Text
Jonathan Hasenburg, Martin Grambow, Elias Grünewald, Sascha Huk, David Bermbach. **MockFog: Emulating Fog Computing Infrastructure in the Cloud**. In: Proceedings of the First IEEE International Conference on Fog Computing 2019 (ICFC 2019). IEEE 2019.

### BibTeX
```
@inproceedings{hasenburg_mockfog:_2019,
	title = {{MockFog}: {Emulating} {Fog} {Computing} {Infrastructure} in the {Cloud}},
	booktitle = {Proceedings of the First {IEEE} {International} {Conference} on {Fog} {Computing} 2019 (ICFC 2019)},
	author = {Hasenburg, Jonathan and Grambow, Martin and Grunewald, Elias and Huk, Sascha and Bermbach, David},
	year = {2019},
	publisher = {IEEE}
}
```

A full list of our [publications](https://www.mcc.tu-berlin.de/menue/forschung/publikationen/parameter/en/) and [prototypes](https://www.mcc.tu-berlin.de/menue/forschung/prototypes/parameter/en/) is available on our group website.

## Run development server
- Depending on your system run `sudo python3 fog_agent.py -hostname localhost -iface en0 -port 5000`
- `ifconfig` lists network interfaces on current machine

## Troubleshooting
- Required python version: 3.6
- `pip3 install -r requirements.txt`
- `pip3 install --trusted-host pypi.python.org pytest-xdist`

## Debugging
- `export FLASK_ENV=development`

## Tests
- `sudo python3 -m unittest properties/tc_config_test.py`
- `sudo python3 -m unittest properties/firewall.py`
- Network interface name is hardcoded in `__init__` methods

## Development on machine created by Nodemanager
- The server is managed by a systemd service called `mfog-agent.service`, the service source can be found in the MockFog-IaC repository

```bash
# list all services that start with fog
systemctl list-units | grep fog

# show the log of the fog agent service
journalctl -u mfog-agent.service

# restart the fog agent service
sudo systemctl restart mfog-fog_agent.service
```
- The source code is at `/opt/mfog-agent`
- eth0 is the management network, eth1 is the communication network
