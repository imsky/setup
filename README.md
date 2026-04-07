# Ivan's tips and config

## Git tips

See [git.md](./git.md).

## Postgres

### psql

* `\du`: show roles
* `\drds`: show group roles and settings
* `\df`: show functions
* `\dn`: show schemas and their owners
* `\dvst`: show views, tables, sequences
* `\dx`: show extensions and which schemas they're in
* `\l`: show databases
* `\dp`: show table permissions
* `\conninfo`: show connection info - database, user, etc.

### Snippets

#### Get current user

```
select current_user;
```

#### Get current database

```
select current_database();
```

#### Get database size

```
select pg_size_pretty(pg_database_size('dbname'));
```

## Create a GIF from video

```sh
vid2gif () {
fps=${2:-24}
bn=$(basename $1)
pf="/tmp/$bn_palette.png"
ffmpeg -y -i $1 -vf "fps=$fps,palettegen" $pf
ffmpeg -i $1 -i $pf -filter_complex "fps=$fps,paletteuse" -f gif - > "$1.gif"
}
```

## Download specific format combination from YouTube

```sh
yt-dlp -S vcodec:h264,acodec:m4a "YOUR_VIDEO_URL"
```

## Download YouTube video as MP3

```sh
yt-dlp --format bestaudio --extract-audio --audio-format mp3 --audio-quality 320k --embed-thumbnail -o '%(title)s.%(ext)s' https://www.youtube.com/watch?v=mUQHGpxrz-8
```

## Convert M4A to Mp3

```sh
ffmpeg -i input.m4a -c:v copy -c:a libmp3lame -q:a 4 output.mp3
```

## Clean output on Node.js

```sh
npm set fund false
npm set audit false
export DISABLE_OPENCOLLECTIVE=1
export ADBLOCK=1
```

## Shell hanging on Ubuntu

Run `bash -x` to see the last line of what's causing the shell to hang.

If it's `nvm`, run `rm "$NVM_DIR/alias/default"` then `nvm alias default node`.

## Set up Apple Mail with Google Workspace

1. Generate app password
2. Add new Other mail account
3. Set incoming to imap.gmail.com
4. Set outgoing to smtp.gmail.com

## Set up Apple Calendar with Google Workspace

* Generate app specific password on Google
* System Preferences -> Internet Accounts -> Add CalDAV account
* Set account type to Advanced
* Set user name to google account (yourusername@gmail.com)
* Set password to app specific password previously generated
* Set server address to: https://calendar.google.com
* Set server path to: /calendar/dav/yourusername@gmail.com/user/
* Set port to: 443
* Put a checkmark in: Use SSL
* Leave "Use Kerberos" unchecked
* Sign in