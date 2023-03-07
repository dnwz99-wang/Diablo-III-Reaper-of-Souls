 

![](pictures/logo.png)

# DiIiS项目

DiIiS是一个功能齐全的开源本地服务器，用于 [暗黑破坏神III：灵魂收割者](https://eu.diablo3.blizzard.com).

## 特色

-实现账户创建系统、授权和大厅

-实现死灵法师

-完全实现的聊天系统和社交

-全面实现宗族制度

-实现了基本的DRLG（副本生成器）

-实现了带有游戏内词缀的物品生成器

-实现了所有职业几乎所有活动能力的基本机制

-实现了一个集合项目系统

-实现了所有故事任务5幕的所有主要脚本

-实现了“冒险模式”的基本脚本和生成器

-实现了“挑战侄子步枪”模式的基础

-为80%的小怪实现了人工智能

-为40%的怪物实现了个人人工智能

-为半数BOSS实施了个人人工智能

-实现了LAN

## Restrictions

- Donate Store implementation is removed.
- NAT support is hidden, but possible ;)

# Installation

## Supported Clients

Each version of the client includes changes to structures, opcodes and attributes.

The currently supported version of the client: **2.7.4.84161**

## Server Deploying

1. Install [PostgreSQL 9.5.25](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads).
2. Create databases in PostgreSQL: `diiis` and `worlds`.
3. Change you account and password in `database.Account.config` and `database.Worlds.conifg`.
4. Restore `worlds.backup` to `worlds` database.
5. Compile by [VS 2019/2022](https://visualstudio.microsoft.com/).
6. [Skip this stage for local game] Copy the [config.ini](configs/config.ini) file to the server folder (It overwrites the default settings):
	- Update the parameter entries with your IP record on the network: `BindIP` and `PublicIP`.
7. Launch wait until server start, it creates a hierarchy.
8. Create user account(s) using console: `!account add Login Password Tag`

### Example:

> !account add username@ YourPassword YourBattleTag

Creates an account with Login `username@`, password `YourPassword` and BattleTag `YourBattleTag`

> !account add username@ YourPassword YourBattleTag owner

Creates an account with Login `username@`, password `YourPassword` and BattleTag `YourBattleTag` with rank `owner`

## Prepare Client

Do this for each client connecting to the server.

1. Get [supported client](#supported-clients) Diablo 3.

2. Install certificate [bnetserver.p12](src/DiIiS-NA/bnetserver.p12), password - `123` (the game verifies the CA root certificates).

3. Setting up redirects client to your server:

	**Method #1 - Hosts**

	  Add redirects to the `hosts` file (`%WinDir%\System32\drivers\etc\hosts`):  
	  `127.0.0.1 us.actual.battle.net`  
	  `127.0.0.1 eu.actual.battle.net`

	  !After the modification the official Battle.Net application will not be able to connect to the server!

	  **Method #2 - Modify main executable file**

	  ```c
	  // Find null-terminated string enum and rewrite with HexEditor to your IP server.
	  eu.actual.battle.net/
	  us.actual.battle.net/
	  cn.actual.battle.net/
	  kr.actual.battle.net/
	  ```

4. Launch client (`x64` or `x86`) with arguments `"Diablo III64.exe" -launch`

5. Login to the game using your credentials.

6. [Skip this stage for local game] After that, when creating a game (in client), indicate the creation of a public game. Other players, when connecting, must also indicate a public game, and at the start they will connect to you.

7. You're in the game world!

## Using Docker

Run `docker-compose up` inside [db](db) folder and continue from the 5th step in section [server](#server-deploying).

# Server Configuration

## Global configuration

Using the configuration file you can easily override the [global world parameters](docs/game-world-settings.md).

## Command system

The command system allows you to get control of the game world if you have rights. A list of commands is available [here](docs/commands-list.md).

# Issues

Check the [report form](docs/report-form.md) before submitting issue, this will help people save time!

# System requirements

|            | **Entry-level**              | **Mid-range**                | **High-end**                 |
| ---------- | ---------------------------- | ---------------------------- | ---------------------------- |
| **CPU**    | Intel Core i5 or AMD Ryzen 5 | Intel Core i7 or AMD Ryzen 7 | Intel Core i9 or AMD Ryzen 9 |
| **Memory** | 4 GB RAM                     | 16 GB RAM                    | 64 GB RAM                    |
| **Disk**   | 500 MB                       | 1 GB                         | 1 GB                         |

# Screenshots

You can see more screenshots [here](SCREENSHOTS.md)

![](pictures/ingame-screen-1.png)

