# Real Engine: A Game Engine for the Real World

[![Build Status](https://travis-ci.org/RealEngine/Real_Engine.svg?branch=master)](https://travis-ci.org/RealEngine/Real_Engine)

## Project Structure

The project consists of:

- **User Interface (`frontend/`):** the frontend GUI
- **Backend Server (`backend/`):** a Python server that runs the GUI and talks to devices
- **Hardware (`hardware/`):** the device firmware and software

## Build and run the backend

If you have Make and Docker installed, you can build the frontend and web service with

```
    $ make build
```

and then run the web server with

```
    $ make run
```
