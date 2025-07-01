### FULLKEKW CHANGELOG

[back](../README.md)

- [Patch 2.1.1](#patch-211)
  - [API](#api)
    - [fullkekw-account-nextjs](#fullkekw-account-nextjs)
    - [fullkekw-userapi](#fullkekw-userapi)
  - [INFRASTRUCTURE](#infrastructure)
    - [fullkekw-account-nextjs](#fullkekw-account-nextjs-1)
    - [fullkekw-userapi](#fullkekw-userapi-1)
    - [fk-authority](#fk-authority)
- [Patch 2.1.0](#patch-210)
  - [INFRASTRUCTURE](#infrastructure-1)
    - [fk-usapi](#fk-usapi)

---------------------------------------------------------------

## Patch 2.1.1

### API
#### fullkekw-account-nextjs

+ /login renamed into /sso

#### fullkekw-userapi

+ /auth via google provider now accept only one method, equals ```provider:google``` instead of ```{method: provider, provider:google}```
+ Every message from endpoint renamed from *msg* into *message*

### INFRASTRUCTURE
#### fullkekw-account-nextjs

+ Renamed from fk-account
+ Reworked architecture to v2.1.1
+ Reworked SSO page (was login)
+ Changed sso page favicon

#### fullkekw-userapi

+ Renamed from fk-usapi
+ Reworked architecture to v2.1.1
+ Reworked token & user & auth controllers
+ Added request tracing
+ Reworked User model & interactions with it
+ Reworked error handling
+ Changed user restrictions (:banned > user:banned; change:username > user:change_username; upload:avatar > user:upload_avatar)
+ Patch username rules have been changed, now accept only alphanumeric values, without special characters
+ Patch username cooldown has been reduced from 30d to 7d
+ Default avatars are now static. Old default avatars that have been removed: 05ba8cc3-3ede-420c-bc0a-2f6ae663b74f, 1ea43878-36f0-416f-9f02-0b6eed54e411 
+ Rewritted tests
+ Fixed VersionError on sessions update (GET /auth/refresh) (2.1.1)

#### fk-authority

- Reworked AcceptedTokens stack, fixed issue with it overflow

---------------------------------------------------------------

## Patch 2.1.0
### INFRASTRUCTURE

**All services**
- Changed default listen IP from static 192.168.0.107 to 127.0.0.1 to reduce bugs with local IP defining

#### fk-usapi
- Fixed avatar uploading
- Fixed CSRF origin




[back](../README.md)