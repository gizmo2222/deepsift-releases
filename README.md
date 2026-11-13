# Deepsift

A co-op digging incremental for one to eight players. You work the night shift in a lamplit Victorian intake hall, under a heap of the city's lost things. Dig into the pile, fill your bag, tip it down a chute for coins, and spend the coins on better tools and carts in the ledger. Somewhere in the heap are the pieces of lost sets: find them, file them in the Claims Archive, and get the Heap cleared. Under the Heap is the Sorting Floor, where you lay out machines and belts to do the sifting for you.

The game is an early prototype and changes often. This page holds its downloads only; the game's own code is private.

## Contents

- [Get the game](#get-the-game)
- [Your first minutes](#your-first-minutes)
- [Playing together](#playing-together)
- [Running a dedicated server](#running-a-dedicated-server)
- [New versions and your saves](#new-versions-and-your-saves)
- [When something goes wrong](#when-something-goes-wrong)

## Get the game

**[Download the newest version](https://github.com/gizmo2222/deepsift-releases/releases/latest)**

1. On that page, under **Assets**, download `Deepsift-win-x64-<version>.zip`. The `Deepsift-server-...` zips are only for running a dedicated server (see below); you do not need them to play.
2. Unzip it anywhere, your Desktop is fine. Nothing is installed and nothing outside that folder and your saves folder is touched.
3. Open the unzipped `Deepsift-win-x64` folder and double-click `Play.cmd`.

You need Windows 10 or 11, 64-bit. Nothing else: .NET and every library the game uses are inside the zip.

The game is not signed, so the first time you run it Windows SmartScreen may say "Windows protected your PC". Choose **More info**, then **Run anyway**. Windows may also ask whether to let the game through the firewall. Allow it on private networks if you plan to host; joining someone else's game does not need it.

What is in the folder:

| File | What it is |
|---|---|
| `Play.cmd` | Starts the game. Use this rather than the exe: if the game ever crashes, it keeps the error on screen so you can read it |
| `Deepsift.Client.exe` | The game itself |
| `Fresh-install.cmd` | Moves your saves and settings aside so the game starts as on a first install (see below) |
| `content\`, `assets\` | The game's numbers, models, textures and sound. Leave them beside the exe |
| `CREDITS.md` | Who made it and what it is made with |

## Your first minutes

The game opens on a title screen:

| Item | What it does |
|---|---|
| Play | Plays a world of your own, carrying on from where you left off |
| The opening | The same, with the Clerk's short story read first |
| New | Starts a fresh world (it asks first) |
| Host | Hosts your world so friends can join it |
| Join | Joins a friend's game or a dedicated server |
| Load | Starts a world from a save slot |
| Settings | Sound, music, mouse sensitivity, field of view, and the Controls page, where every key can be changed |

The first time a world starts, the Clerk reads a short opening; any key skips it. After that, a help card lists the essentials. **F1** brings it back at any time.

| Key | What it does |
|---|---|
| W A S D, mouse | Walk and look |
| Left mouse button | Dig with the tool in hand |
| Right mouse button | The tool's second action: Hands pick up one thing, the Shovel pries crust loose, the Rake sifts a patch, the Magnet sweeps up loose pieces |
| 1 to 4 | Pick a tool (or buy a locked one when you can afford it) |
| E | Hands: take a key, open a chest, push a cart, file the set pieces you carry at their cabinet |
| F | Bag: empty it at a chute, load it into a cart |
| Tab | The ledger: the upgrade tree |
| X (hold) | Inspect what you are aiming at, and which tool digs it best |
| F1 | The help card |
| Esc | The menu: save, load, settings, quit to the title |

A game controller works too; the Controls page shows its buttons.

The loop: dig until the bag is full, carry it to a chute and press F to empty it, and spend the coins in the ledger. A brass mark and a soft chime say when an upgrade is affordable. The goal at the top left says what the group is working toward. When a set piece turns up, carry it in your hands to its wing's cabinet on the north wall and press E to file it. The Clerk will say a line the first time something new happens.

## Playing together

Up to eight players share one world. One machine owns the world (the host) and everyone else joins it. There are two ways to host:

- **From the game.** One player picks **Host** on the title screen and plays as normal. The world lives on their PC, so it is there only while they are playing.
- **A dedicated server.** A small program with no window and no player of its own holds the world on any Windows or Linux machine, so it stays up when everyone leaves. See [Running a dedicated server](#running-a-dedicated-server).

### Hosting from the game

Pick **Host** on the title screen. It asks for:

| Field | What to put |
|---|---|
| Port | `7777` unless you have a reason to change it |
| Password | A word your friends will type to get in. Leave it empty for none (fine on a private network, not on the open internet) |
| Most players | `8` |

Then tell your friends your address and the password.

### Joining

Pick **Join** on the title screen and fill in:

| Field | What to put |
|---|---|
| Address | The host's address, for example `100.64.1.2` or `100.64.1.2:7777`. The port defaults to 7777 |
| Name | What the others see you as. Empty uses your Windows user name |
| Password | The host's password, or empty if there is none. It is never saved, so you type it each time |

The address and name are remembered for next time. If the join fails, the same page says why: nobody answering at that address, a wrong password, or a different version.

**Everyone must run the same version.** The host checks this on every join and refuses anyone on another version, naming the version it runs. When a new version comes out, the host and every player update together.

### Reaching the host

Your friends' computers have to be able to reach the host's port (TCP 7777). Pick whichever fits:

| Setup | How | Notes |
|---|---|---|
| Same house or LAN | Join the host's local address, such as `192.168.1.20` | The host's firewall must allow the game on private networks |
| [Tailscale](https://tailscale.com) (easiest over the internet) | Everyone installs Tailscale and joins the same tailnet. Join the host's Tailscale address (`100.x.y.z`) | Nothing is opened to the internet and there is no router setup |
| Port forwarding | The host forwards TCP 7777 on their router to their PC. Friends join the host's public IP address | Anyone on the internet can reach the port, so always set a password |
| A dedicated server on a rented machine | See the next section | Stays up all the time |

The password never travels over the network in readable form, and five wrong guesses from one address lock that address out for a minute.

## Running a dedicated server

The dedicated server hosts a world with no window and no player of its own. Players join it exactly as they would join a friend. It saves the world every minute and when it stops, so it can run for weeks and pick up where it left off after a restart.

Use it when you want the world to be there whenever anyone feels like playing, or when no one's home connection is good for hosting.

### What you need

- A machine that stays on: a spare Windows PC, a home server, or a rented Linux VPS. It needs no graphics card and no screen.
- The server zip **of the same version as the players' game**, from the same release page: `Deepsift-server-win-x64-<version>.zip` for Windows or `Deepsift-server-linux-x64-<version>.zip` for Linux. Nothing else is needed: .NET is inside the zip.
- TCP port 7777 reachable by the players (see [Reaching the host](#reaching-the-host)). On a VPS, open it in the provider's firewall and the machine's own.

### On Windows

1. Unzip `Deepsift-server-win-x64-<version>.zip` into a folder of its own, for example `C:\Deepsift`.
2. Open PowerShell in the `Deepsift-server-win-x64` folder (in Explorer: Shift + right-click inside the folder, then **Open PowerShell window here**).
3. Set the password and start the server:

```powershell
$env:DEEPSIFT_PASSWORD = "pick-a-word"
```

```powershell
.\Server.cmd
```

The window shows the server's log: who joins and leaves, and any refused connection with its address. Leave it open while the server runs. When Windows asks whether to let `Deepsift.Server.exe` through the firewall, allow it.

To stop the server, press **Ctrl+C** in its window. It says goodbye to the players and saves.

### On Linux

The Linux server is self-contained: it runs on a bare Ubuntu or Debian image with nothing installed. These commands run in the Linux machine's shell, not in PowerShell. Replace `<version>` with the version number.

```sh
wget https://github.com/gizmo2222/deepsift-releases/releases/download/v<version>/Deepsift-server-linux-x64-<version>.zip
```

```sh
sudo apt install unzip
```

```sh
unzip Deepsift-server-linux-x64-<version>.zip
```

`unzip` may warn that the zip "appears to use backslashes as path separators". That is expected; the files come out in the right folders.

```sh
cd Deepsift-server-linux-x64
```

```sh
sudo ufw allow 7777/tcp
```

(Skip the `ufw` line if the machine does not use ufw; open the port in your provider's firewall either way.)

```sh
DEEPSIFT_PASSWORD="pick-a-word" sh server.sh
```

To keep the server running after you log out, start it inside `tmux` (or `screen`): run `tmux`, start the server, then press **Ctrl+B** then **D** to leave it running. `tmux attach` brings its console back. **Ctrl+C** stops it and saves.

Run it as an ordinary user, not root. It only writes inside its own folder.

### The password

`Server.cmd` and `server.sh` refuse to start without a password, since a server is usually reachable from the internet. Give it one of two ways:

- the `DEEPSIFT_PASSWORD` environment variable, as above (keeps the word out of your shell history and the process list), or
- `--password "pick-a-word"` after the script's name.

To run with no password on purpose, for example on a tailnet where only your friends can reach it, add `--open`:

```powershell
.\Server.cmd --open
```

### Options

Anything after `Server.cmd` or `server.sh` is passed to the server. The scripts already pass `--host 7777 --grid full --save saves\main`.

| Option | What it does |
|---|---|
| `--password WORD` | The password players must give |
| `--open` | Run without a password on purpose |
| `--save DIR` | Where the world is kept (default `saves\main` beside the server). Use a different folder for a second world |
| `--fresh` | Start a new world in the save folder instead of loading the one there. The old world is overwritten at the next save, so copy it away first |
| `--seed N` | The new world's seed (default 1). Only matters with `--fresh` or an empty save folder |
| `--bots N` | Bot teammates who dig alongside the players (default 0) |
| `--max-players N` | The most players at once (default 8) |
| `--listen ADDRESS` | Listen on one address only, for example your Tailscale address, so the port is not open on other networks |
| `--trust NAME` | A player who may use the cheat console (repeat for each; see below) |
| `--help` | Lists every option |

For example, a server with two bots that only listens on its Tailscale address:

```powershell
.\Server.cmd --bots 2 --listen 100.64.1.2
```

### The server console

While it runs, the server's window takes these commands:

| Command | What it does |
|---|---|
| `trust NAME` | Lets the player with that display name use the in-game cheat console |
| `untrust NAME` | Takes it away |
| `trusted` | Lists the trusted players |
| `cheat NAME [ARGS]` | Runs a cheat as the host. `cheat help` lists them |

Trusted names are kept in `trusted.txt` in the save folder, so they survive a restart. A name is tied to the first player who joins under it, so trust names only on a server with a password, or have that player join before you trust them.

### Saves, backups and moving a world

The world lives in the save folder, `saves\main` beside the server. To back it up, copy that folder; the server saves every minute, so a copy taken while it runs is at most a minute old. Stop the server first for an exact copy.

To move a world you have been playing on your own PC to the server, stop the server, then copy the contents of your save slot (for example `%LOCALAPPDATA%\Deepsift\saves\autosave`) into the server's `saves\main` folder, replacing what is there. The next start loads it.

### Updating the server

When a new version comes out:

1. Stop the server with Ctrl+C.
2. Unzip the new server zip into a new folder.
3. Copy the old `saves` folder into the new `Deepsift-server-...` folder.
4. Start the new one the same way.

Players must update their game too, or the server refuses them. Keep the old folder until the new one has run for a while; it is your way back.

## New versions and your saves

New versions come often. To update, download the new zip and unzip it; you can delete the old folder once the new one runs. Your settings and worlds are not in the game folder but in `%LOCALAPPDATA%\Deepsift` (paste that into Explorer's address bar to open it), so a new version carries on from where you were.

| What | Where |
|---|---|
| Your world, saved every minute and on quit | `%LOCALAPPDATA%\Deepsift\saves\autosave` |
| Slots you saved from the menu | `%LOCALAPPDATA%\Deepsift\saves\<slot name>` |
| Settings, controls, achievements | `%LOCALAPPDATA%\Deepsift` |

A guest never saves: the host owns the world, and everyone's progress in it is kept on the host's machine.

To start over as on a first install, double-click `Fresh-install.cmd` in the game folder. It moves everything above aside into a dated folder rather than deleting it, so renaming that folder back restores your old world.

Once in a while a new version cannot read an old world. The game then keeps the old save beside the new one, starts a new world and says so.

## When something goes wrong

| Problem | What to try |
|---|---|
| "Windows protected your PC" | Choose **More info**, then **Run anyway**. The game is not signed |
| The join fails with no host at that address | Check the address and that the host is running. Over the internet, check the port forward or that you are both on Tailscale. Try from the host's own machine with `127.0.0.1` to rule out the game itself |
| The join page says the host runs another version | Download the version it names; the host and everyone else must match |
| The join page says the password is wrong | Ask the host for it again. After five wrong tries your address is locked out for a minute |
| The server will not start and asks for a password | Set `DEEPSIFT_PASSWORD` or pass `--password WORD`, or `--open` for none |
| The game crashed | It writes `crash-<date and time>.txt` into `%LOCALAPPDATA%\Deepsift\saves`. Send that file to whoever gave you the game, with a line on what you were doing |

## Older versions

Every version, with what changed in it, is on the [Releases](https://github.com/gizmo2222/deepsift-releases/releases) page.
