# BinBot Innovation: Sustainable Disposal Network

A mobile bin concept for collecting waste from children and pets, with a vacuum mechanism for small waste particles. Built for **Smart India Hackathon 2025**, Problem Statement **25111**, by **Team Terrabyte**.

## Concept

Conventional bins are fixed, and small debris around people and pets is hard to collect. BinBot is a mobile bin that:

- moves to where waste is,
- collects small particles with a vacuum mechanism,
- monitors its own fill level and reports it to a cloud dashboard so collection routes can be planned, and
- uses a safety interlock so the vacuum never runs while a child or pet is close to the intake.

## Technology areas

IoT, sensors, computer vision (OpenCV), AI, Python, embedded systems, mobile applications, and cloud/IoT connectivity.

## Project status

The project went through four rounds of internal evaluation and was not selected in the fourth round. This repository documents the design and the software prototype built during the hackathon.

## Repository layout

```
src/binbot/
  config.py              Tunable thresholds and device settings
  main.py                Control loop tying sensors, safety, vacuum and telemetry together
  sensors/ultrasonic.py  Distance sensing for fill level (simulated driver included)
  vision/particles.py    OpenCV contour-based detection of small particles
  vision/safety.py       Pluggable person/pet detector interface for the safety interlock
  actuators/vacuum.py    Vacuum controller with proximity interlock
  cloud/telemetry.py     Telemetry payload builder and publisher interface
tests/                   Unit tests for safety logic, fill calculation and telemetry
docs/architecture.md     System design and field-research notes
```

## Running

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
PYTHONPATH=src python -m binbot.main --cycles 5
PYTHONPATH=src python -m unittest discover -s tests -v
```

The prototype runs on a laptop with simulated sensors. Hardware drivers (GPIO for the ultrasonic sensor, motor driver for the vacuum) sit behind small interfaces so they can be swapped for real devices on a Raspberry Pi or similar board.

## Safety principles

1. The vacuum never starts if a person or pet is detected inside the safety radius.
2. If the proximity reading is unavailable, the vacuum does not run.
3. The bin stops and reports a fault rather than guessing.

## Team

Team Terrabyte, Smart India Hackathon 2025.
