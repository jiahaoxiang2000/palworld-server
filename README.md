# Palworld Server

here we use the [palworld-server-docker](https://github.com/thijsvanloef/palworld-server-docker) docker image to run a palworld server.

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