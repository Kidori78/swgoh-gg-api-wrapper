# swgoh-gg-api-wrapper
Google Sheet Library to help with making calls to swgoh.gg api without having to get your own api-key. It has 2 main functions you can choose between for making calls to the api. There is also a class available to use that has all endpoints mapped out to easily grab specific data.

## Table of Contents
1. [Installing](#installing)
2. [Available Functions](#available-functions)
   - [.fetchData](#fetchdataurl)
   - [.fetchAPI](#fetchapiurl-throwerror-returnnulls)
3. [Available Class](#available-class)
4. [Class Methods](#class-methods)
   - [.getPlayers()](#getplayersallycode)
   - [.getGuilds()](#getguildsguildid)
   - [.getGuildRosters()](#getguildrostersguildidthrowerrorreturnnulls)
   - [.getUnits()](#getunits)
   - [.getCharacters()](#getcharacters)
   - [.getShips()](#getships)
   - [.getGear()](#getgear)
   - [.getAbilities()](#getabilities)
   - [.getStatDefinitions()](#getstatdefinitions)
   - [.getDatacrons()](#getdatacrons)
   - [.getDatacronSets()](#getdatacronsets)
   - [.getDatacronAffix()](#getdatacronaffix)
   - [.getDatacronTemplates()](#getdatacrontemplates)
5. [Using to fix your current project](#using-to-fix-your-current-project)

<br />

## Installing
**STEP 1:** In your current project go to the ***Menu Bar => Extensions => Apps Script***\
**STEP 2:** In the side bar click the **+** next to ***Libraries***, then add the following Script ID and select the latest version.
```
1yDBhGEqlpEk9wSVBSu6nrtJ0a4eft1QpCeofMFeWVe5KeYRnhabzH2DX
```

<br />

## AVAILABLE FUNCTIONS
To use these functions you must use the library name followed by the function.\
***E.G. MyLibraryName.fetchData(url);***

### .fetchData(url)
<details><summary>This is a simple fetch that just grabs the data from the provided URL, formats it in JSON and returns it.</summary>

#### Parameters
`url` _String_\
The full url (endpoint) to get the data from.

```js
  let player = SWGOHGGAPIWrapper.fetchData("https://swgoh.gg/api/player/596966614");
  let units = SWGOHGGAPIWrapper.fetchData("https://swgoh.gg/api/units");
```
</details>

### .fetchAPI(url, throwError, returnNulls)
<details><summary>A more complex fetch that allows for doing async calls on numerous urls at once ( uses fetchAll() ) along with error logging, error throwing, and handling partially missing data calls. This will also take the standard single URL like the other function.</summary>

#### Parameters
`url` _String or Array_\
The full url (endpoint) to get the data from.

`throwError` _Bool_ | **Optional**\
Flag to indicate throwing an error if a guild member has a null ally code. Default is true.

`returnNulls` _Bool_ | **Optional**\
Flag to indicate returning null for player profiles that have a null ally code. Default is false.
  
```js
  let guild = ggAPI.getGuildRosters("596966614");
  let guilds = ggAPI.getGuildRosters(["xsafGSFSfsad-Gdsa","987654321"]);
```
</details>

<br />


## AVAILABLE CLASS
To use this class you must first initialize it using the function **.startAPICall()**.\
**Usage Examples**
```js
//Instantiate Class
const ggAPI = SWGOHGGAPIWrapper.startAPICall();
//Grab player data using ally code
let player = ggAPI.getPlayers("596966614");
//Grab guild data using ally code or guild id
let guild = ggAPI.getGuilds("596966614");
//Grab guild data with member rosters using ally code or guild id
let guildRoster = ggAPI.getGuildRosters("596966614");
```

## Class Methods

### .getPlayers(allyCode)
<details><summary>Returns the specified player profile from the api.</summary>

#### Parameters
`allyCode` _String or Array_\
List of player ally code(s) to retrieve data for.

```js
  let player = ggAPI.getPlayers("596966614");
  let players = ggAPI.getPlayers(["123456789","987654321"]);
```
</details>


### .getGuilds(guildID)
<details><summary>Returns the specified guild profiles from the api.</summary>
  
#### Parameters
`guildID` _String or Array_\
List of guild id(s) or ally code(s) to retrieve guild data for.

```js
  let guild = ggAPI.getGuilds("596966614");
  let guilds = ggAPI.getGuilds(["xsafGSFSfsad-Gdsa","987654321"]);
```
</details>


### .getGuildRosters(guildID,throwError,returnNulls)
<details><summary>Returns the specified guild profiles including all member rosters from the api.</summary>
  
#### Parameters
`guildID` _String or Array_\
List of guild id(s) or ally code(s) to retrieve guild data for.

`throwError` _Bool_ | **Optional**\
Flag to indicate throwing an error if a guild member has a null ally code. Default is true.

`returnNulls` _Bool_ | **Optional**\
Flag to indicate returning null for player profiles that have a null ally code. Default is false.
  
```js
  let guild = ggAPI.getGuildRosters("596966614");
  let guilds = ggAPI.getGuildRosters(["xsafGSFSfsad-Gdsa","987654321"]);
```
</details>

### .getGuildRosters()
Returns the specified guild profiles including all member rosters from the api.

### .getUnits()
Returns data for all playable units.

### .getCharacters()
Returns data for all playable characters.

### .getShips()
Returns data for all playable ships.

### .getGear()
Returns data for all gear.

### .getAbilities()
Returns data for all unit abilities.
    
### .getStatDefinitions()
Returns data to convert stat enums into stat names

### .getDatacrons()
Returns all data about Datacrons. Sets, Templates, and Affix abilities.

### .getDatacronSets()
Returns data about Datacron sets.

### .getDatacronAffix()
Returns data about Datacron abilities.

### .getDatacronTemplates()
Returns data about Datacron templates used.

<br />

## Using to fix your current project
If you are using someone elses sheet first reach out to them to see if there is an updated version of the sheet. If there is not or this is your own sheet you can use the following code to fix your current sheet.

#### Using this library file
Search the code for UrlFetchApp and then replace it with the following
```js
  //Example old code
  const options = {
    method: 'GET',
    contentType: 'application/json'
  };
  let response = UrlFetchApp.fetch(url, options);
  
  //Example new code
  let response = SWGOHGGAPIWrapper.fetchData(link)
```

#### Using your own API Key
Search the code for UrlFetchApp then add or modify the options argument.
```js
const options = {
  method: 'GET',
  contentType: 'application/json',
  headers: {
    x-gg-bot-access: your-access-key
  }
};
let data = UrlFetchApp.fetch(url, options);
```

<br />

## Reviewing Code
The actual code can be viewed here for safety and learning purposes: [SWGOH GG API Wrapper - Apps Script](https://script.google.com/home/projects/1yDBhGEqlpEk9wSVBSu6nrtJ0a4eft1QpCeofMFeWVe5KeYRnhabzH2DX/edit)
