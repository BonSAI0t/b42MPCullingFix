# Project Zomboid Build 42 Multiplayer Culling Fix

## ⚠️ WARNING ⚠️

**Use this at your own peril. DO NOT REPORT BUGS IF YOU CANNOT REPLICATE THEM WITHOUT THIS MOD**

This modification changes core game networking behavior. Any issues you encounter may be caused by this modification and should not be reported to the developers unless you can reproduce them on an unmodified server.

---

## What This Does

This modification disables client-initiated zombie deletion in Project Zomboid Build 42 multiplayer servers.

### Background

In vanilla Project Zomboid, clients automatically send requests to delete distant zombies as part of the game's zombie count optimization system (`ZombieCountOptimiser`). This is a designed game mechanic to maintain performance by culling zombies that are far from players.

This modification makes the server ignore those deletion requests while maintaining full network protocol compatibility.

---

## Installation

### Prerequisites
- Java JDK installed (for the `jar` command)
- Access to your Project Zomboid server JAR file
- Backup of your original `projectzomboid.jar`

### Steps

1. **Backup your original JAR file:**
   ```bash
   cp projectzomboid.jar projectzomboid.jar.backup
   ```

2. **Navigate to this directory** (where the `zombie/` folder is located)

3. **Update the JAR with the patched class:**
   ```bash
   jar uf /path/to/projectzomboid.jar zombie/network/packets/character/ZombieDeletePacket.class
   ```

   Replace `/path/to/projectzomboid.jar` with the actual path to your server's JAR file.

4. **Verify the patch was applied:**
   ```bash
   jar tf /path/to/projectzomboid.jar | grep "ZombieDeletePacket.class"
   ```

   Expected output: `zombie/network/packets/character/ZombieDeletePacket.class`

5. **Restart your server**

---

## What Changed

The `ZombieDeletePacket` class was modified to make the server ignore zombie deletion requests while maintaining protocol compatibility. The server will still properly consume and acknowledge the packets, preventing any network errors or desyncs.

---

## Reverting

To revert this modification, simply restore your backup:

```bash
cp projectzomboid.jar.backup projectzomboid.jar
```

Then restart your server.

---

## Technical Details

- **Modified Class:** `zombie.network.packets.character.ZombieDeletePacket`
- **Server-side only:** No client modifications required
- **Network compatible:** Works with vanilla clients
- **Game Version:** Build 42

---

## License

Use at your own risk. This is an unofficial modification and is not supported by The Indie Stone.
