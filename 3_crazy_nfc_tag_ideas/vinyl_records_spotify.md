# Vinyl Records on Spotify

Example record automation:

```yaml
alias: Van Halen
description: ""
triggers:
  - trigger: tag
    tag_id: Van Halen
conditions: []
actions:
  - action: script.play_music_on_spotify
    data:
      spotify_album_id: 7DdEbYFPKTZ8KB4z6L4UnQ
mode: single
```

Spotify playing script:

```yaml
alias: Play music on Spotify
description: ""
fields:
  spotify_album_id:
    name: Spotify Album ID
    description: Enter just the album ID (e.g. 0gv5aiVS1WBUZOKeb7YawE)
    required: true
    selector:
      text: {}
sequence:
  - action: media_player.turn_on
    metadata: {}
    data: {}
    target:
      entity_id:
### Change these media entities to your own TV/stereo/player.
### Same with related entities beloe.
        - media_player.sony_xbr_75x90ch
        - media_player.tsr_700_ad3c21
        - media_player.nvidia_shield
  - action: media_player.select_source
    metadata: {}
    data:
      source: Spotify
    target:
      entity_id: media_player.nvidia_shield
  - action: media_player.select_source
    target:
      entity_id: media_player.spotify_thomas
    data:
      source: SHIELD
  - action: media_player.play_media
    target:
      entity_id: media_player.spotify_thomas
    data:
      media:
        media_content_id: spotify:album:{{ spotify_album_id }}
        media_content_type: album
        metadata: {}
  - action: media_player.media_play
    target:
      entity_id: media_player.spotify_thomas
    data: {}
```
