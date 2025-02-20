# @distube/spotify

A DisTube custom plugin for supporting Spotify URL. Upgraded to support new Distube >= v3.0.0alpha/beta

## Status: beta

Requires DisTube v3.0.0-beta/alpha

# Feature

This plugin grabs the songs on Spotify then searches on YouTube and play with DisTube.

# Installation

```sh
npm install @distube/spotify
```

# Usage

```js
const Discord = require("discord.js");
const DisTube = require("distube");
const SpotifyPlugin = require("@distube/spotify");
const client = new Discord.Client();
const distube = new DisTube(client, {
	searchSongs: 10,
	emitNewSongOnly: true,
	plugins: [new SpotifyPlugin({ parallel: true })],
});

// Now distube.play can play spotify url.

client.on("message", (message) => {
	if (message.author.bot) return;
	if (!message.content.startsWith(config.prefix)) return;
	const args = message.content
		.slice(config.prefix.length)
		.trim()
		.split(/ +/g);
	const command = args.shift();
	if (command === "play") distube.play(message, args.join(" "));
});
```

## Documentation

### SpotifyPlugin([options])

-   `options.parallel`: Default is `true`. Whether or not searching the playlist in parallel.
-   `options.emitPlaySongAfterFetching`: Default is `false`. Emit `playSong` event before or after fetching all the songs.
    > If `false`, DisTube plays the first song -> emits `playSong` events -> fetches all the rest\
    > If `true`, DisTube plays the first song -> fetches all the rest -> emits `playSong` events
