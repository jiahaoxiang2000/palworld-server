# Palworld Server

here we use the [palworld-server-docker](https://github.com/thijsvanloef/palworld-server-docker) docker image to run a palworld server.

## Server Configuration

This server is [configured](https://docs.palworldgame.com/settings-and-operation/configuration/) for an **easier and more relaxed** gameplay experience with the following modifications:

### Experience & Progression
- **3x Experience Rate** - Level up faster
- **2x Pal Capture Rate** - Easier to catch Pals
- **2x Resource Drop Rate** - More materials from gathering and enemies

### Survival & Comfort
- **50% Slower Hunger/Stamina Decay** - Less micromanagement
- **2x Health Regeneration** (3x during sleep) - Faster recovery
- **50% Lighter Items** - Carry more without encumbrance

### Combat & Defense
- **50% Less Damage Taken** - More forgiving combat
- **50% More Damage Dealt** - Faster enemy defeats
- **Item-only Death Penalty** - Keep your Pals when you die
- **Invaders Disabled** - Peaceful base building

### Base Management
- **2x Work Speed** - Pals work much faster
- **20 Base Workers** (increased from 15) - More productive bases
- **2x Building Health** - Stronger structures
- **80% Slower Building Decay** - Less maintenance required

### Quality of Life
- **24-hour Egg Hatching** (reduced from 72 hours) - Faster breeding
- **24-hour Item Persistence** - Dropped items last longer
- **More Frequent Auto-saves** - Better save protection
- **Faster Day/Night Cycle** - Less waiting

### Server Access
- **Admin Password**: `admin`
- **Server Password**: `palworld`
- **RCON Port**: 25575
- **Public Port**: 8211

## Starting the Server

To start the Palworld server:

```bash
docker compose up -d
```

To stop the server:

```bash
docker compose down
```

To view server logs:

```bash
docker compose logs -f
```

## Configuration Changes

If you want to modify the server settings, edit the file:
`palworld/Pal/Saved/Config/LinuxServer/PalWorldSettings.ini`

After making changes, restart the server:

```bash
docker compose down
docker compose up -d
```

## Manually restore from a backup

Locate the backup you want to restore in `/palworld/backups/` and decompress it.
Need to stop the server before task.

```bash
docker compose down
```

Delete the old saved data folder located at `palworld/Pal/Saved/SaveGames/0/<old_hash_value>`.

Copy the contents of the newly decompressed saved data folder `Saved/SaveGames/0/<new_hash_value>` to `palworld/Pal/Saved/SaveGames/0/<new_hash_value>`.

Replace the DedicatedServerName inside `palworld/Pal/Saved/Config/LinuxServer/GameUserSettings.ini` with the new folder name.

```ini
DedicatedServerName=<new_hash_value>  # Replace it with your folder name.
```

Restart the game. (If you are using Docker Compose)

```bash
docker compose up -d
```