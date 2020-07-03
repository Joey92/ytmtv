# YouTube music TV

Turns your youtube music videos into your own TV station.
Sometimes I like to play music from youtube on the TV at parties or hangouts.
Often times youtube plays some random stuff and I miss the artists name.
It's basically displaying song information while playing the music video as an overlay, like a music TV channel has.

It's deployed as a single page app at joey92.github.io.
Example: http://joey92.github.io/?v=lX44CAz-JhU

This is a proof of concept. Everything needs to be built around the youtube player, which has a lot of power.

The web page needs to be full screen. Don't fullscreen the youtube player or else you will not get the overlay.

## Features
- [-] Displays a banner at the beginning and at the end of the video

## Upcoming features
- [] Load the actual song info or the banner
- [] Enable playlists
- [] Customize the banner
- [] Integrate the youtube data api
- [] Show comments of the video as if they were sms's sent to a TV station
- [] Add a twitter feed with a specific hash tag

## With Server hosting at some point
- [] Server hosting the playlist
- [] User submitting music videos
- [] Users voting on the next song

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).
