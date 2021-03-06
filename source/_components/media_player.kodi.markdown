---
layout: page
title: "Kodi"
description: "Instructions how to integrate Kodi into Home Assistant."
date: 2015-06-22 11:00
sidebar: true
comments: false
sharing: true
footer: true
logo: kodi.png
ha_category: Media Player
featured: true
ha_release: pre 0.7
ha_iot_class: "Local Push"
---


The `kodi` platform allows you to control a [Kodi](http://kodi.tv/) multimedia system from Home Assistant.

To add Kodi to your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
media_player:
  - platform: kodi
    host: 192.168.0.123
```

Configuration variables:

- **host** (*Required*): The host name or address of the device that is running XBMC/Kodi.
- **port** (*Optional*): The HTTP port number. Defaults to 8080.
- **tcp_port** (*Optional*): The TCP port number. Defaults to 9090. Used for websocket connections to Kodi.
- **name** (*Optional*): The name of the device used in the frontend.
- **proxy_ssl** (*Optional*): Connect to kodi with HTTPS and WSS. Defaults to `false`. Useful if Kodi is behind an SSL proxy.
- **username** (*Optional*): The XBMC/Kodi HTTP username.
- **password** (*Optional*): The XBMC/Kodi HTTP password.
- **turn_off_action** (*Optional*): The desired turn off action. Options are `none`, `quit`, `hibernate`, `suspend`, `reboot`, or `shutdown`. Default `none`.
- **enable_websocket** (*Optional*): Enable websocket connections to Kodi via the TCP port. Defaults to `true`. The websocket connection allows Kodi to push updates to Home Assistant and removes the need for Home Assistant to poll. If websockets don't work on your installation this can be set to `false`.


### {% linkable_title Service `kodi_add_to_playlist` %}

Add music to the default playlist (i.e. playlistid=0).

| Service data attribute | Optional | Description |
| ---------------------- | -------- | ----------- |
| `entity_id` | no | Name(s) of the Kodi entities where to add the media.
| `media_type` | yes | Media type identifier. It must be one of SONG or ALBUM.
| `media_id` | no | Unique Id of the media entry to add (`songid` or `albumid`). If not defined, `media_name` and `artist_name` are needed to search the Kodi music library.
| `media_name` | no| Optional media name for filtering media. Can be 'ALL' when `media_type` is 'ALBUM' and `artist_name` is specified, to add all songs from one artist.
| `artist_name` | no | Optional artist name for filtering media.

