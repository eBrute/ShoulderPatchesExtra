# ShoulderPatchesExtra
**ZycaR (c) 2016**

When the official shoulder patches are not enough and server administrators want to reward some players according how they behave on server the shoulder patches extra is the solution. To enable ShoulderPatchesExtra add ``"2bc45759"`` to the list of mods running on server and configure.

Beautiful part is, that it will not override official patch player choose to wear on his shoulder.
## Configuration guide
#### Basics

The configuration of ShoulderPatchesExtra consist of three main parts:
- **Shoulder Patches Texture** .. the image(s) containing tiled shoulder patches
- **Material File** .. the text file which tells the game where to find shoulder patches image and how many rows & columns of patch contains
- **Patches Config File** .. the json file for configuration player->patch relation.

#### Shoulder Patches Texture
*This part cannot be modified with original workshop mod, any modification will be classified as violation of consistency check. To modify this part please contact the author.*


To minimise complexity, disk space and something called *"draw calls"* (internal engine's magic) the patches are tiled in one image. It's preferred to arrange patches into square (i.e. 2x2, 4x4, ...)

> It's not restricted to arrange all patches in one big line, but you will probably suffer with poor performance ...

Please note, that the mod uses not only one but two patches textures. The reason is simple, ns2 engine is not very flexible when it comes to transparency. Therefore one texture **spe_emissive.dds** contains colour information, the second one **spe_opac.dds** contains information known as alpha or opacity or transparency.

Emissive file: ``..\models\marine\patches\spe_emissive.dds``\
Opacity file: ``..\models\marine\patches\spe_opac.dds``

#### Material File
*This part cannot be modified with original workshop mod, any modification will be classified as violation of consistency check. To modify this part please contact the author.*

Next part of shoulder patches mod is material file. This text file tells engine location, where to find emmisive and opacity texture and describe tilling of patches. Describe how are patches arranged in how many rows and columns.

Material file: ``..\models\marine\patches\shoulder_patch.material``
```
...
speOpacityMap = "models/marine/patches/spe_opac.dds"
speEmissiveMap = "models/marine/patches/spe_emissive.dds"
speRows = 2
speCols = 2
```

#### Patches Config File
Finally last but not least we have config file description. After reading all those not so enjoyable previous parts (did you actually read them?). If you didn't read them properly then please do. It's highly recommended and will help to understand *patch index section* of config file.

After first run of game with mounted mod, the default config is created:\
Config file: ``%appdata%\Natural Selection 2\ShoulderPatchesConfig.json``

The config part named **BadgeIndex** is dictionary to map "group_name" to "patch index" (will explain later).
To get proper group for player the Shine mod configuration is used. Please note, that shine mod must be properly configured and running on the server. Fortunately when you don't have Shine, or you want to override some crazy patch for specific player you can use Users part of config.

Config part **Users** is another dictionary to assign "group_name" to player by it's "steamid" (overrides Shine config).

Example of config file:
```json
{
  "BadgeIndex":{
    "none":0,
    "admin_group": 1,
    "moderators": 2,
    "idiots": 3
  },
  "Users":{
    "90000000000001":"none",
    "438225": "moderator"
  }
}
```

##### BadgeIndex
BadgeIndex is position of patch on texture. Index with 0 occupied left-top corner, iIndex 1 is second column to right on same top-most row. This continues to bottom-right corner.

> Please always consider index 0 as no-patch position. This index is used by mode to show no patch for not configured players (without group assigned).

### ShoulderPatchesExtra Mod ID - 2573eb73
```sh
Server.exe -mods "2bc45759"
```

### SteamWorkshop link
http://steamcommunity.com/sharedfiles/filedetails/?id=734287705