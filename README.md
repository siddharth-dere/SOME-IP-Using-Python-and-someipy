# Assignment 1: Virtual Vehicle Speed Service Using SOME/IP (`someipy`)

Python automotive service-oriented communication system implementing **SOME/IP** and **SOME/IP-SD** on Ubuntu Linux using `someipy` and Wireshark.

## Interface Specification

| Element | Identifier | Transport / Payload |
| :--- | :--- | :--- |
| `VehicleSpeedService` | Service `0x1234`, Instance `0x5678`, Major `1` | UDP (`127.0.0.1:3000`) |
| `GetSpeed` (Method) | `0x0001` | Request: `0 B` / Response: `uint16` (`2 B`, km/h) |
| `SpeedChanged` (Event) | `0x8001` (Event Group `0x0001`) | Notification every `2 s`: `uint16` (`2 B`, km/h) |
| Service Discovery | `224.224.224.245:30490` | Cyclic Offer every `2000 ms`, TTL `5 s` |

## Repository Structure

```text
someip-python-assignment/
├── src/          # vehicle_speed_interface.py, vehicle_speed_service.py, cluster_client.py
├── config/       # someipyd.json
├── captures/     # assignment1-someip.pcapng
└── images/       # Wireshark and terminal validation screenshots
```

## How to Run

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install someipy
someipyd --config config/someipyd.json          # Terminal 1
python src/vehicle_speed_service.py             # Terminal 2
python src/cluster_client.py                    # Terminal 3
```
