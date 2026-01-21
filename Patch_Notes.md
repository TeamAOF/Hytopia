# 21th of January

### Fixes
Fixed huge lag spike every 5 second due to server reading ``YmmersiveMelodiesRegistry``, which contains all the custom MIDI files. This does NOT work for such a large server we're running.

---

# 20th of January

### Changes
* Added skills leaderboard (use **/xp**, head to the leaderboard tab)
* Added EyeSpy (See **info** about blocks when looking at them)
* Added enchantments, yes you heard me.
* Lowered max claims to **9**, claims will be buyable this weekend. This is to reduce the huge claims of nothingness.
* Added #useful-commands, its for well... Useful commands to use on the server.
* More progress on spawn, we're getting there! Next up is portals hub.
* Added XP support for Wan's weapons.

### Fixes
* Fixed a CRITICAL performance bug with HUD placements.
* Fixed certain interactions not being protected in claims, like crops etc.
* Fixed voting rewards for (<https://hytaleonlineservers.com/server-hytopia.590>)
* Fixed Wayback Charm not working.

---

# 18th/19th of January

### Changes
* Added Skills (Open GUI with /xp)
* Added a custom difficulty system with 3 options **(Normal, Intermediate & Hard)**, server is set to **Intermediate**. This is to go on par with the new skills system, I hope yall enjoy it.
```
Intermediate:
85% Player Damage
90% Player Health
125% Mob Damage
```
* Improved claims colors & usability
* Moved to new permissions system, this will allow for much better configuration going forward.
* Added **Persistent Signature Move** which makes it so once you charge up a signature move (Default: Q), any "unequipping" actions doesn't make you lose that signature move charge.
* Fixed voting rewards for (<https://hytaleserverlist.me/server/hytopia.42007>)
* Improved voting lookup, now has a proper GUI (/vote)
* Many performance improvements and fixes has been implemented to reassure a smoother playing experience.
* Fixed chat announcements stacking up if server was lagging.
* Added relics weapons (Wans Wonder Weapons)
* Added more spellbooks!
* Fixed black lines sometimes appearing in water.
* Work has been started on spawn, check it out! (Thanks Maddmollyy)

---

# 17th of January

### Changes
* Updated to Update 1
* Added /shops & /money

You can set up a shop with /myshop manager, you need to create a tab (which is essentially a shop) and then you can hold an item and do /myshop add <tab> <buy price> <sell price> ... if it doesn't show up in /shops, do /myshop open

quick distinction: the buy price is the price of someone buying the item you are listing, the sell price is the price of someone selling the item listed TO you. the price you choose is for 1 quantity.

---

# 16th of January

### Fixes
Pickup Item Crash (Critical)
When a player disconnects while picking up an item, the world thread crashes and kicks ALL players in that world.

Error: ``NullPointerException`` in ``PickupItemSystem.tick()`` - null ``targetRef``
Fix: Safely marks corrupted pickup items as finished before they crash the server
RespawnBlock Crash (Critical)
When a player breaks a bed or sleeping bag, they get kicked from the server.

Error: ``NullPointerException`` in ``RespawnBlock$OnRemove`` - null ``respawnPoints`` array
Fix: Initializes the respawn points array before Hytale's buggy code runs
ProcessingBench Window Crash (Critical)
When a player breaks a campfire or crafting table while another player has it open, they get kicked from the server.

Error: ``NullPointerException`` in ``BenchWindow.onClose0`` - null ref during window close
Fix: Clears the windows map before the crash-causing close handlers run
Instance Exit Missing Return World (Critical)
When a player exits an instance (dungeon, cave, etc.) and the return world data is corrupted, they get kicked from the server.

Error: ``IllegalArgumentException`` in ``InstancesPlugin.exitInstance`` - Missing return world
Fix: Tracks player position before entering instances and uses it as fallback destination
Empty Archetype Entities (Monitoring)
Logs entities with corrupted/empty component data for debugging. These don't crash but indicate world data issues.

Chunk Memory Bloat
Hytale doesn't properly unload chunks when players move away, causing unbounded memory growth and eventual OOM crashes.

Symptoms: Server memory grows from 4GB to 14GB+ while players fly around; chunks never decrease
Example: Player loads 5,735 chunks, only 317 are in view radius, 5,400+ stay in memory forever
Fix: ``ChunkCleanupSystem`` runs on the main thread every 30 seconds to trigger Hytale's internal chunk cleanup
Results: Observed 77% reduction in loaded chunks (942 → 211) after fix
