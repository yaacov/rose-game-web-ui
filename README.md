# rose-game-web-ui
[ROSE game](https://github.com/RedHat-Israel/ROSE) web based graphical user interface.

This component implement a web based graphical user interface for the ROSE game.

<p align="center">
  <img src="web-ui.png" alt="rose game components diagram" width="400"/>
</p>

ROSE project: https://github.com/RedHat-Israel/ROSE

## Requirements

 Requires | Version | |
----------|---------| ---- |
 Podman (or Docker) | >= 4.8 | For running containerized |
 Node   | >= 20  | For running the code loally |

## ROSE game components

Component | Reference |
----------|-----------|
Game engine | https://github.com/RedHat-Israel/rose-game-engine |
Game web based user interface | https://github.com/RedHat-Israel/rose-game-web-ui |
Game car driving module | https://github.com/RedHat-Israel/rose-game-ai |

## Running the web based graphical user interface loally

Clone this repository, and make sure you have a game engine running.

Run the user interface:

```bash
# Get help
npm start -- --help

# Run the server (connect to a game engine running on http://127.0.0.1:8880)
npm start -- -hp http://127.0.0.1:8880 -wp ws://127.0.0.1:8880 -p 8080
```

## Running ROSE game components containerized

### Running the game engine ( on http://127.0.0.1:8880 )

``` bash
podman run --rm --network host -it quay.io/rose/rose-game-engine:latest
```

### Running the game web based user interface ( on http://127.0.0.1:8080 )

``` bash
podman run --rm --network host -it quay.io/rose/rose-game-web-ui:latest
```

### Running your self driving module, requires a local `driver.py` file with your driving module. ( on http://127.0.0.1:8081 )

``` bash
# NOTE: will mount mydriver.py from local directory into the container file system
podman run --rm --network host -it \
  -v $(pwd)/mydriver.py:/mydriver.py:z \
  -e DRIVER /mydriver.py \
  quay.io/rose/rose-game-ai:latest
```
