# Project Zomboid Build 42 Multiplayer Culling Fix

### ⚠️⚠️⚠️ EXTRA DOUBLE WARNING ⚠️⚠️⚠️
Not compatible / updated for b42.14.0
Will freeze your server
Currently dealing with a situation at work, don't even have my gaming PC setup right now. Will look for someone to carry the torch / patch it, hopefully should be a simple patch.

## ⚠️ WARNING ⚠️

**Use this at your own peril. DO NOT REPORT BUGS IF YOU CANNOT REPLICATE THEM WITHOUT THIS MOD**

This modification changes core game networking behavior. Any issues you encounter may be caused by this modification and should not be reported to the developers unless you can reproduce them on an unmodified server.

---

## What This Does

This modification disables client-initiated zombie deletion in Project Zomboid Build 42 multiplayer servers.

### Background

In vanilla Project Zomboid, clients automatically send requests to zombies you can't see as part of the game's zombie count optimization system (`ZombieCountOptimiser`). This is a designed game mechanic intended to maintain performance by culling zombies that are far from players.

This modification makes the server ignore those deletion requests.

---

## Installation

### Prerequisites
- Access to your Project Zomboid server JAR file
Example:
pzserver@bon-test-zom-svr01:~/serverfiles/java$ ls
projectzomboid.jar  serialize.lua  stdlib.lbc  stdlib.lua

- Backup of your original `projectzomboid.jar`
- **Either:** Java JDK installed (for `jar` command) **OR** 7-Zip/WinRAR (for GUI method)

**If you don't know what you're doing - use the 7-Zip/WinRAR method
### Method 1: Using `jar` Command (Recommended)

**Linux/macOS:**

1. **Backup your original JAR file:**
   ```bash
   cp projectzomboid.jar projectzomboid.jar.backup
   ```

2. **Navigate to this repository directory** (where the `/java` folder is located)

3. **Update the JAR with the patched class:**
   ```bash
   jar uf /path/to/projectzomboid.jar zombie/network/packets/character/ZombieDeletePacket.class
   ```

4. **Verify the patch was applied:**
   ```bash
   jar tf /path/to/projectzomboid.jar | grep "ZombieDeletePacket.class"
   ```

5. **Restart your server**

**Windows:**

1. **Backup your original JAR file:**
   ```cmd
   copy projectzomboid.jar projectzomboid.jar.backup
   ```

2. **Navigate to this repository directory** in Command Prompt or PowerShell

3. **Update the JAR with the patched class:**
   ```cmd
   jar uf C:\path\to\projectzomboid.jar zombie\network\packets\character\ZombieDeletePacket.class
   ```

   Example for Steam installation:
   ```cmd
   jar uf "C:\Program Files (x86)\Steam\steamapps\common\ProjectZomboid\java\projectzomboid.jar" zombie\network\packets\character\ZombieDeletePacket.class
   ```

4. **Restart your server**

### Method 2: Using 7-Zip or WinRAR (Windows)

If you don't have Java JDK installed:

1. **Backup your original JAR file**

2. **Open the JAR file:**
   - Right-click on `projectzomboid.jar`
   - Select **7-Zip → Open archive** (or **Open with WinRAR**)

3. **Navigate to:** `zombie\network\packets\character\`

4. **Delete the existing class file:**
   - Select `ZombieDeletePacket.class`
   - Press Delete and confirm

5. **Add the patched class file:**
   - Drag and drop `ZombieDeletePacket.class` from this repository into the `character\` folder
   - Confirm the replacement
   - **IMPORTANT:** Ensure the path is `zombie\network\packets\character\ZombieDeletePacket.class`

6. **Close the archive** (changes save automatically)

7. **Restart your server**

---

## What Changed

The `ZombieDeletePacket` class was modified to make the server ignore zombie deletion requests. The server will still properly consume and acknowledge the packets, preventing any network errors or desyncs.

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
