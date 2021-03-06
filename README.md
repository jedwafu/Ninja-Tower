ZOMG!!#@# Now playable on http://ninjatower.eu !

# By the Gods, what is this?

Ninja Tower is a crossover of a 2D MOBA/ARTS/DOTA with smash'em game. It was to feature advanced teamplay along with pure smashing fun. It would have certainly met that goal if not lack of sufficiently available pixel artists. We could provide only a single character - too little for any advanced tactics to be. Therefore - thinking up a new game that would not require as much pixeling around, and be certainly more fun - we decided to scrap Ninja Tower and make it available under a BSD 3-clause license, for other people to study the innards of a - working, as you might see on movies - fast-paced network game.

# What does it consist of?

## The Server Part

Server part is written in PyPy-ready Python. It is advised for at least **sakura** to run under PyPy - it's uneconomically (but feasibly) CPU-hungry when ran under CPython.

**Sakura** is the shard server. It is started up to service a single game - clients connect to it, have fun, and when sakura detects that end of game condition (sufficient smash'up) was met, it halts itself and writes match result to file, ready for reaping by lshardmgr.

Sakura expects a resource folder - the same that clients will have on their PCs - available somewhere on the server to read physics constraints, characters and maps. Path to it is specced in startup "battle preparation file" (path to which is passed by command line on startup).

Due to multi-tier hierarchy of server - shards can be spawned on different machines to provide load balancing, a two-tier solution was thought up.

**Cshardmgr** is unique. There's only one. It satisfies lobbyapp's requests to allocate a shard (sakura) by dispatching it to connected slaves, ie. **lshardmgrs**. These in turn fire up shards, allocate ports for them, take care if they throw up, and relay results back to the server (lobbyapp)

**Lobbyapp** is the thing launcher connects to. You can find someone to play here, pick your character, and then entire server-allocation and game-managing process will be fired by lobbyapp. It is written in a nice transaction-fashioned way, has some unittests, and requires [Satella](https://github.com/henrietta/satella). It talks (networkily) with clients in an elegant SSL+JSON language.

## The Client Part

**patcher_launcher** have two folder in it. They are written in C#.<br>
    -Patcher is a program which automaticaly download updates from server.<br>
    -Launcher is a program which allow you log in game and choose queue. It run directly **main_exe**.<br>

**main_exe** is a main battle engine written in C++ with allegro5.

## Game editors

**Map_cutter** is a program which allow big map to be cut on smaller pieces. Piece have size 512x512.

**Heroes_editor_v1** is a program which allows you edit heroes but is deprecated. **Game_editor_v2** is his successor.

**Map_editor_v1** is a program which allows you edit maps but is deprecated. **Game_editor_v2** is his successor.

**Game_editor_v2** is a program which allows you edit maps, heroes and shots.

## Other stuff

**unused_images** is a folder that contains images which was unused in game.

**gameplay_movies** is folder that contain movies from game. You can watch 2 of 3 on youtube.<br>
    -http://www.youtube.com/watch?v=FROgdSAQUwc first gameplay without sound and poor GUI in game.<br>
    -http://www.youtube.com/watch?v=yj6sJk268m0 second gameplay with sound and nice GUI in game.

# I've seen enough source. Give me the docs.

Sorry, they are only available in Polish. On the gripping side, it's in MediaWiki markup syntax, so safe for human consumption. Consult polish_documentation directory for that. What may interest you most are the protocol specifications - both "inter-shardmgr", launcher-lobbyapp and game client-sakura ones.

# License? Copyright holders?

See License.txt

# I want to continue this project!

And we'll give you our best blessings. If you fail to bootstrap it by hand, consult License.txt and nag somebody. The two first guys on the lists are coders and may (or may not) help.
