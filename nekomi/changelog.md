### NEKOMI.CLUB CHANGELOG

[back](../README.md)

- [Patch 2.1.2](#patch-212)
  - [API](#api)
    - [nekomi-api](#nekomi-api)
  - [INFRASTRUCTURE](#infrastructure)
    - [nekomi-api](#nekomi-api-1)
    - [nekomi-nextjs](#nekomi-nextjs)
- [Patch 2.1.1](#patch-211)
  - [API](#api-1)
    - [nekomi-api](#nekomi-api-2)
  - [INFRASTRUCTURE](#infrastructure-1)
    - [nekomi-api](#nekomi-api-3)
    - [nekomi-nextjs](#nekomi-nextjs-1)
- [Patch 2.1.0](#patch-210)
  - [API](#api-2)
    - [nekomi-api](#nekomi-api-4)
    - [nekomi-uploads](#nekomi-uploads)
    - [nekomi-media](#nekomi-media)
  - [INFRASTRUCTURE](#infrastructure-2)
    - [nekomi-api](#nekomi-api-5)
    - [nekomi-nextjs](#nekomi-nextjs-2)
    - [nekomi-uploads](#nekomi-uploads-1)
    - [nekomi-media](#nekomi-media-1)
    - [nekomi-bot](#nekomi-bot)
    - [nginx](#nginx)

---------------------------------------------------------------

## Patch 2.1.2

### API
#### nekomi-api

+ Fixed /anime/stats

### INFRASTRUCTURE
#### nekomi-api

+ Fixed notifications handlers
+ Added IMDB, Ashdi, Jikan API integrations
+ Added Ashdi VOD service
+ Added extending nekomi episodes with ashdi
+ Added pulling myanimelist episodes meta
+ Added anime DMCA restrict

#### nekomi-nextjs

+ Added anime DMCA restrictions
+ Added nekomi player HLS support
+ Disabled link prefetch
+ Added tracing $api requests in logs
+ Fixed nekomi player playback start on page load, IOS playsInline, setting idle state when video paused


## Patch 2.1.1

### API
#### nekomi-api

+ Removed parseTogetherRoom from GET /user/:query
+ Removed GET /user/validate
+ Removed POST /user/together
+ Removed DELETE /user/together/:id
+ Renamed PATCH /user/me into /user
+ Renamed GET /user/linkTelegram/token into /user/link/telegram/token
+ Renamed GET /user/linkTelegram into /user/link/telegram
+ Renamed GET /user/linkTelegram/verify into /user/link/telegram/verify
+ Removed ?metadataOnly from each endpoint

### INFRASTRUCTURE
#### nekomi-api
+ Added fix user lib anime documents (some users may have unavailable anime documents it their libs)
+ Refactored anime & user controllers, user model
+ Reworked errors throwing
+ Reworked anime service & user model tests
+ Reworked Routes
+ Fixed general development issues
+ Fixed user avatar / username sync with fullkekw-sso
+ Fixed failing myanimelist sync on client request (sync calls on both main and metadataOnly requests)

#### nekomi-nextjs
+ Reworked CSRF token forgery
+ Reworked header / mobile menus
+ Migrated @fullkekw/fkw-popup to @fullkekw/popup
+ Optimized page loading by removing jsrassing lib
+ Fixed general development issues
+ Fixed logout on session expire

---------------------------------------------------------------

## Patch 2.1.0
Patch 2.1.0 touches everything that belongs to nekomi Anime (was Title) model & interactions with it. Including anime API, user watch experience & series uploading. Reworked everything that can be reworked, deleted everything that can be deleted. Optimized inner workflows & rework testing

### API
#### nekomi-api
- GET /search (global search) **removed**, use /user/search, /dubber/search, /anime/search instead respectively 
- GET /anime/search now return max dubbed ep for each result
- GET /anime/:query response document name changed from ```title``` into ```anime``` .```parseDubbers``` now ```fetchDubbers```. New property ```metadataOnly``` will return only metadata-related data. Added ```fetchRelated``` property to fetch related anime documents. 
- GET /anime/total is now /anime/all. ```renewed``` is now ```updated```. Added ```fullfilled``` prop with documents where both malId and status are present
- GET /anime/home_wrapped was refactored into /anime/featured
- GET /user/:query ```parseRoles``` now ```parseCapabilities```
- GET /dubber/all **removed**, use /dubber/search?q=~all instead
- PATCH /anime/:uuid is now PATCH /anime. UUID property moved in body
- GET /anime/all renamed into /anime/stats (old routes will be removed in 2.1.1)

#### nekomi-uploads
- Added GET /:id method

#### nekomi-media
- Removed nofile property from GET /:id
- Fixed client-side files caching, change GET /:id status code (206 > 200)



---

### INFRASTRUCTURE

**All services**
- Changed default listen IP from static 192.168.0.107 to 127.0.0.1 to reduce bugs with local IP defining

#### nekomi-api
> [!IMPORTANT]
> Title model is now Anime model. Everything associated with Title model was reworked/renamed

NEW:
- uuid: was id
- slug: was code
- broadcast: new broadcast details
- genres: reworked
- rate: reworked, was ageRate
- status: reworked
- season: reworked
- media: reworked type
- studios: reworked
- malId: was mal_id, type changed from string | null to number | null
- malSyncedAt: new field that contain last sync with mal timestamp
- pictures: new field that contain anime pictures
- related: new field that contain related anime's id's
- posterAdapt: new field that contain dubber id who adapted poster
---

+ Added rickroll for invalid requests
+ Added sync anime with myanimelist
+ Added user remove watch progress
+ Added safeGetByQuery in each ModelService
+ Added MyAnimeList API integration (2.1.0)
+ Added MyAnimeList fetch seasonal anime util (2.1.0)

- Refactored handlers into single-purpose utils
- Refactored architecture (renamed files n folders)
- Refactored relative paths into absolute (~/)
- Migrated eslint config to mjs
- Reworked Mocking & testing
- Reworked error codes in enums, turn more errors into generic
- Reworked Anime Service, write tests for each **set** method
- Fixed anime stats (was /all) updated (2.1.0)

+ Removed deprecated code
+ Disabled online poll & watch together

#### nekomi-nextjs
+ Added Anime API integration
+ Added nekoplayer continue episode progress preload (2.1.0)

+ Updated interactions with Anime API & GET /user
+ Updated user profile, home page & Client-Server logic
+ Reworked watch page & anime patcher
+ Reworked search (client/server), replace global search with category-related
+ Updated nekoplayer (was kekwplayer) UI & logics
+ Updated @fullkekw/fkw-popup package to the latest version
+ Updated contacts page
+ Updated watch page ui (2.1.0)

- Fixed $api Axios instance ECONNRESET error
- Fixed ```secondsToReadable``` breaks on hours (in pretty return H:[empty])
- Fixed nekoplayer watch progress. Add sync on path & visibility changes & add full progress remove
- Fixed episodes uploading (2.1.0)
- Fixed player does not update user watch progress if he not natively pause/play (2.1.0)
- Fixed patcher anime stats (2.1.0) & patcher search open anime by slug and not uuid
- Fixed watch page display zero uploaded episodes

+ Disabled online poll & watch together

#### nekomi-uploads
- Added husky
- Added fullkekw-authority API integration

+ Updated to v2.1.0
+ Changed resize dimensions for photo/title/poster from 600x800 (1.3) to 800x1120 (1.4)
+ Changed video/title/episode config. Default bitrate 2600k > 3200k; Short bitrate (<300s) 6000k > 5000k
+ Refactored interfaces
+ Refactored handlers into utils
+ Refactored tests

- Fixed some uploads paths were undefined
- Fixed DELETE /:id throws 404 error when upload is not exist

+ Removed mocking
+ Removed types: video/srt, video/srt-temp with their handlers (workflow, purgeTempSRTs)

#### nekomi-media
+ Updated to v2.1.0
+ Configured husky

#### nekomi-bot
+ Updated to v2.1.0
+ Changed sending messages from template based into HTTP request based

#### nginx
+ Extended nekomi-media cache (7d > 31d)
+ Remove repeated Cache-Control header
+ Remove Last-Modified="" header

---------------------------------------------------------------




[back](../README.md)