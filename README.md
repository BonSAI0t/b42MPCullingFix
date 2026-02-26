# Project Zomboid Build 42 Multiplayer Culling Fix

## ⚠️ WARNING ⚠️

Use this at your own peril. 

**DO NOT REPORT BUGS TO THE INDIE STONE IF YOU CANNOT REPLICATE THEM WITHOUT THIS MOD**

This modification changes core game networking behavior. Any issues you encounter may be caused by this modification and should not be reported to the developers unless you can reproduce them on an unmodified server.

---

### Background

In Project Zomboid, clients automatically send requests to delete the zombies you can't see as part of the game's zombie count optimization system (`ZombieCountOptimiser`) which is a performance measure to cull the zombies that are far away from the player. But it also deletes the zombies right behind the player if there is too many zombies in the cell.

## What This Does

- Makes the server ignore the zombie deletion requests. The server will still properly consume and acknowledge the packets, preventing any network errors or desyncs.
- No client modifications required
- Achieved by commenting out the loop within the `ZombieDeletePacket` class which deletes zombies 

---

## Installation

### Prerequisites
- Access to your Project Zomboid server JAR file
Example:
pzserver@bon-test-zom-svr01:~/serverfiles/java$ ls
projectzomboid.jar  serialize.lua  stdlib.lbc  stdlib.lua

**If you are not familiar with bash or cmd - use the Method 2**

### Method 1: Using `jar` Command (Requires Java JDK installed)

**Linux/macOS:**

1. **Backup your original JAR file:**
    ```bash
    cp projectzomboid.jar projectzomboid.jar.backup
    ```

2. **Clone this repo and navigate to the directory** (change the VERSION to the version of your server)
    ```bash
    git clone https://github.com/BonSAI0t/b42MPCullingFix && cd b42MPCullingFix/VERSION
    ```

3. **Update the JAR with the patched class:**
    ```bash
    jar uf /path/to/projectzomboid.jar zombie/network/packets/character/ZombieDeletePacket.class
    ```

4. **Restart your server**

**Windows:**

1. Backup your original JAR file:
    ```cmd
    copy projectzomboid.jar projectzomboid.jar.backup
    ```

2. Clone this repo and navigate to the directory (change the VERSION to the version of your server)
    ```cmd
    git clone https://github.com/BonSAI0t/b42MPCullingFix && cd b42MPCullingFix\VERSION
    ```

3. Update the JAR with the patched class:
    ```cmd
    jar uf C:\path\to\projectzomboid.jar zombie\network\packets\character\ZombieDeletePacket.class
    ```

    Example for Steam installation:
    ```cmd
    jar uf "C:\Program Files (x86)\Steam\steamapps\common\ProjectZomboid\java\projectzomboid.jar" zombie\network\packets\character\ZombieDeletePacket.class
    ```

4. **Restart your server**

### Method 2: Using 7-Zip or WinRAR

1. Backup your original JAR file

2. Right-click on** `projectzomboid.jar` and open with **7-Zip** or **WinRAR**

3. Navigate to: `zombie\network\packets\character\` and delete `ZombieDeletePacket.class`

5. Drag and drop `ZombieDeletePacket.class` of the correct version in place of the deleted file

6. Close the archive (changes save automatically)

7. Restart your server

**If the correct version is not present, try the closest version**

## Reverting

To revert this modification, simply restore your backup:

**Linux/macOS:**
```bash
mv projectzomboid.jar.backup projectzomboid.jar
```

**Windows:**
```cmd
move projectzomboid.jar.backup projectzomboid.jar
```

Then restart your server.

---

## License

Use at your own risk. This is an unofficial modification and is not supported by The Indie Stone.
