# Tizen IPTV Player

A small, free IPTV player for Samsung smart TVs (Tizen), written in plain HTML and JavaScript.
It plays the public playlists from [iptv-org/iptv](https://github.com/iptv-org/iptv) and lets you
browse them with the TV remote.

> This project is not affiliated with iptv-org. This repository contains no channels, streams or
> playlists of its own: it only reads playlists you point it to.

## Features

- Plays HLS (`.m3u8`) streams with Samsung's AVPlay
- Loads M3U playlists: your own `playlist.m3u` (bundled in the app) plus Italy from iptv-org at start-up
- **Country browser**: pick any country from the iptv-org list and load its channels on demand
- Category tabs (from the playlists' `group-title`), an "all channels" tab and **favourites**
- Remembers the last channel and the favourites
- If a channel does not start, it skips to the next one by itself
- Everything works with the default remote keys

## Remote control

| Key | Playing | Channel list open |
| --- | --- | --- |
| OK | open the list | play the channel (country tab: load the country) |
| OK, held ~0.7 s | | add/remove favourite |
| Up / Down | previous / next channel | move in the list |
| Left / Right | | previous / next tab |
| Back | exit | close the list |

Tabs: Favourites, All, Countries, My list, then the countries you loaded and the categories.

## Tested on

Samsung UE50TU7070 (2020, 7 Series, Tizen 5.5). Other Tizen TVs that support AVPlay should work,
but I could not try them. Reports are welcome.

## Install

You need a PC, a free Samsung developer account, and the TV on the same network as the PC.

1. **Developer mode on the TV**: Smart Hub → Apps, type `12345` with the remote, switch it on and
   enter the IP address of your PC. Restart the TV.
2. **VS Code**: install the *Tizen TV* extension (`tizensdk.tizentv`).
3. Create an empty Tizen TV web project, then replace its `index.html`, `config.xml` and add
   `playlist.m3u` and `icon.png` from this repository
   (or open this folder as the project).
4. **Certificate**: *Tizen TV: Run Certificate Manager* → Samsung certificate, *public* privileges,
   and tick your TV's DUID. The TV must be on and in developer mode.
5. *Tizen TV: Build Signed Package* creates a `.wgt` file, then install it on the TV.

Never publish the `.wgt` or the certificate files: they contain your certificate chain and the
identifier of your TV. The provided `.gitignore` already leaves them out.

## Configuration

At the top of the script in `index.html`:

- `PLAYLISTS`: playlists loaded at start-up
- `COUNTRIES`: countries offered in the *Countries* tab (iptv-org's `countries/<code>.m3u`)

Add your own channels to `playlist.m3u`, two lines per channel (`#EXTINF:-1,Name` and the URL).

## Known limitations

- The interface text is in Italian for now
- Channel logos are read from the playlists but not shown yet
- Big country playlists can take a while to load
- Many public streams are dead or geo-blocked: that depends on the playlists, not on this app
- No programme guide (EPG)

## Legal

Play only streams you are allowed to watch. The app does not host or redistribute any video.

## License

Public domain, see [LICENSE](LICENSE) (Unlicense).
