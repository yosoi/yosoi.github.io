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

