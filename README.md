# Ansible-galicaster role

Ansible role for galicaster installation and configuration.

This role is suited for galicaster community edition and will install galicaster from the .deb package hosted on the teltek site.

## Requirements

None

## Role Variables

A list of all possible variables, at the moment you need to define to complete list in your host or group vars.

```
galicaster_package: http://webfiler.teltek.es/webfiler/galicaster/galicaster_1.4.1_all.deb
matterhorn:
  host: localhost:8080
  user: matterhorn_system_account
  pass: opencast
  workflow: full
  workflow_params: 'trimHold:false;archiveOp:true'
  multiple_ingest: False
galicaster:
  user: galicaster
  group: galicaster
  enable_admin: True
  default_profile: default
  enable_quit: True
  legacy: False
  manual_ingest: manually
  scheduled_ingest: immediately
  capturename: CA01
  allow_manual: True
  allow_pause: True
  allow_stop: True
  log_path: /var/log/galicaster/galicaster.log
  log_level: INFO
  log_rotate: True
  plugins:
    - name: rest
      value: True
    - name: checkrepo
      value: True
  capture_camera:
    name: Camera
    device: v4l2
    flavor: presenter
    active: True
    location: /dev/video1
    file: camera.avi
    caps: video/x-raw-yuv,framerate=24/1,width=720,height=576
  capture_screen:
    name: Screen
    device: v4l2
    flavor: presentation
    active: True
    location: /dev/video0
    file: screen.avi
    caps: video/x-raw-yuv,framerate=24/1,width=1024,height=768
  capture_audio:
    name: pulseaudio
    device: pulse
    location: default
    file: sound.mp3
    flavor: presenter
    vumeter: True
    amplification: 1.0
    active: True
  profiles:
    - VisionAV-HD-43
    - VisionAV-SD-43
    - VisionAV-Slides-43
```

### Plugins

```
plugins:
  - name: rest
    value: True
  - name: checkrepo
    value: True
```

You can provide a list of plugins that need to be included in the galicaster config file for your specific host. This section needs to be improved to make it possible to also define the plugin settings.

### Profiles

A list of profiles that will be placed in the profiles directory. In your playbook files directory there should be a directory named profiles with a file named as defined in this list.

```
- Galicaster Playbook
|
|---files
    |
    |---profiles
        |
        |---VisionAV-HD-43
        |---ScreenOnly
        |---....
|---roles
|....
```

## Contact

Issues or feature requests can be created in this repository.
