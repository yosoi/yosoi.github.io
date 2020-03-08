# Publishing CLI Programs to PyPI
Using Python, [fire](https://google.github.io/python-fire/guide/), and [poetry](https://python-poetry.org/), you can create a simple console application and publish it to [PyPI](https://pypi.org/). Once published to PyPI, users will be able to install your project using [pip](https://pip.pypa.io/en/stable/).

Install [poetry](https://python-poetry.org/):

`curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3`

Navigate to the directory where you want to create your project.

Then, to create a project named `app`, run:

`poetry new app`

Navigate into the newly created `app` folder. Inside, you will see a handful of files, a sub-folder named `tests`, and another sub-folder named `app`.

Create a script named `main.py` in the `app` sub-folder.

Let's install dependencies before writing any code. We will use [fire](https://google.github.io/python-fire/guide/) to create the interface for this console application. To add `fire` as a dependency, run:

`poetry add fire`

To install your dependencies, run:

`poetry install`

Now that `fire` is installed, open `main.py` and paste the following code.

````
from fire import Fire

def greet(name):
    msg = "Hello, {}".format(name)
    print(msg)

def activate():
    Fire({
        "greet": greet
    })
````

Inside of the `app` sub-folder is a script called `__init__.py`. Open it and paste the following code:

````
from .main import activate
````

To learn more about Python modules and `__init__.py`, [click here](https://docs.python.org/3/tutorial/modules.html#packages).

Once you have updated `__init__.py`, navigate to your project folder and open `pyproject.toml`. This file contains information about your program and is used by `poetry` for configuration purposes.

Add the following lines to `pyproject.toml`:

````
[tool.poetry.scripts]
app = 'app:activate'
````

To learn more about `pyproject.toml`, [click here](https://python-poetry.org/docs/pyproject/).

To begin the publishing process, [create an account](https://pypi.org/account/register/) on PyPI.

Once you have created an account, navigate to your account settings page. Create a new API Token and copy it to your clipboard.

Update your credentials locally by running:

`poetry config pypi-token.pypi {your token value goes here}`

Finally, build and publish your project by running:

`poetry publish --build`

Run the following command to confirm that your project (named `app`, in this case) is online:

`pip3 search app`

Once you have verified that your project is listed, you can install `app` with pip. To do so, run:

`sudo pip3 install app`

Once you have installed `app`, run the following command:

`app greet {your name goes here}`

If everything went smoothly, your app should greet you:

`Hello, Yosoi`

To publish changes to your package, first increment the version number in `pyproject.toml`. Then, run:

`poetry publish --build`

To update an installed pip package, run:

`sudo pip3 install {package name goes here} -U`

Check out [shrimpy](https://github.com/yosoi/shrimpy) if you learn by example.

# Choosing a License
[This helpful document](https://choosealicense.com/) explains how to choose a license for your software and can be summed up as follows:

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

