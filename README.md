# Choosing a License
[This helpful document]() explains how to choose a license for your software and can be summed up as follows:

* [MIT](https://choosealicense.com/licenses/mit/) lets users do almost anything with your software.
* [GNU GPLv3](https://choosealicense.com/licenses/gpl-3.0/) lets users do almost anything with your software *except* distribute closed-source versions.
* [The Unlicense](https://choosealicense.com/licenses/unlicense/) lets users do whatever they want with your software.

# Versions
[This helpful document](https://semver.org/) explains how to version your software:

    Given a version number MAJOR.MINOR.PATCH, increment the:

    MAJOR version when you make incompatible API changes,
    MINOR version when you add functionality in a backwards compatible manner, and
    PATCH version when you make backwards compatible bug fixes.


# Phaser + Sockette = Realtime Multiplayer HTML Games
[Sockette](https://github.com/lukeed/sockette) provides an extremely simple way to connect your Phaser game to a websocket URL.
````
import Sockette from "...";
import onClose from "...";
import onError from "...";
import onMaximum from "...";
import onMessage from "...";
import onOpen from "...";
import onReconnect from "...";

class TestScene extends Phaser.Scene {
    constructor() {
      super({
        key: "TestScene"
      });
    }
    
    create() {
      this.connection = new Sockette(
        "...your websocket url goes here...",
        {
          timeout: 5e3,
          maxAttempts: 10,
          onopen: e => onOpen(e, this),
          onmessage: e => onMessage(e, this),
          onreconnect: e => onReconnect(e, this),
          onmaximum: e => onMaximum(e, this),
          onclose: e => onClose(e, this),
          onerror: e => onError(e, this)
        }
      );
    }
}

export default TestScene;
````

# Serverless Multiplayer Services
Clients connect to a WebSocket API. The Websocket API routes requests to a suite of Lambda functions. The Lambda functions interact with a DynamoDB table and relay messages back to clients via the Websocket API. This system has zero overhead costs because services are only payed for when they are used (with millisecond accuracy). The modular, event-driven nature of the system means that the system naturally scales itself to meet demand.

# Hey
An anonymous RPG-style chatroom game. This project idea was chosen as a gentle introduction to Phaser and WebSockets. [link to project board](https://trello.com/b/1djlEMae/hey)

# Why HTML Games?
HTML games are easy for players to access and share from any device, including public computers. HTML games can also be repackaged as mobile applications.

