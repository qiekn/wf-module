# 创建 Warface 服务器启动级别 XML 文件的说明

## 该文件的目的是什么？

该文件是服务器所必需的，以便：

1. 在界面中地图能够正确显示，特别是地图的名称、描述、图标、模式以及是否会显示；
2. 在启动时具有正确的模式、时间段（TOD）；
3. 具有必要的奖励值和要求；
4. 遵循各种限制；
5. 还有许多其他细节；

没有这个文件，无法通过界面启动地图，如果可以启动，则地图很可能没有必要的设置和功能。

## 为 PvP 地图创建文件

整体结构：

```xml
<mission name="" time_of_day="" game_mode="" game_mode_cfg="" uid="" release_mission="" clan_war_mission="" only_clan_war_mission="" channels="" rating_game_mission="" event_mission="">
  <Basemap name=""/>
  <TimeOfDay file="" start="" end="" speed="" />
  <UI>
    <Description text="" icon=""/>
    <GameMode text=""/>
  </UI>
  <Sublevels mission_flow="default" win_pool="" lose_pool="" draw_pool="" score_pool=""/>
  <TimeDependency min_time="" full_time="" />
  <KillDependency min_kills="" full_kills="" />
  <Objectives/>
  <Teleports/>
</mission>
```

### 开始于主要部分 `mission`:

`name` - 地图的英文名称或本地化名称的关键字；

`time_of_day` - 地图上的时间，以十进制格式表示（例如，如果地图上的时间应该是 \[08:15\]，则在此处写为 `time_of_day="8.25"`）；

`game_mode` - 模式的技术名称；

`game_mode_cfg` - 模式 CFG 文件的完整名称（例如，如果您的地图用于死亡竞赛，则写为 `game_mode_cfg="ffa_mode.cfg"`）；

`uid` - 地图的唯一标识符（唯一标识符是一个 128 位整数，可以使用小写字母、数字、短横线作为分隔符，格式为：`********-****-****-****-************`。可以在网站上生成：[Free Online GUID Generator](https://www.guidgenerator.com/)）；

`release_mission` - 地图在游戏中是否可用（`release_mission="1"` - 可用，`release_mission="0"` - 不可用）；

`clan_war_mission` - 地图在公会战中是否可用（`clan_war_mission="1"` - 可用，`clan_war_mission="0"` - 不可用）；

`only_clan_war_mission` - 地图是否仅在公会战中可用（`clan_war_mission="1"` - 是，`clan_war_mission="0"` - 否）；

`channels` - 地图将在哪些频道中可用进行游戏（"pvp_newbie" - 新手，"pvp_skilled" - 普通，"pvp_pro" - 老手。可以通过逗号列出，例如：`channels="pvp_newbie, pvp_skilled, pvp_pro"`）；

`rating_game_mission` - 是否可以在评分比赛的轮换中使用地图（`rating_game_mission="1"` - 是，`rating_game_mission="0"` - 否）；

`event_mission` - 是否可以在 PvP 活动中使用该地图（`event_mission="1"` - 是，`event_mission="0"` - 否）；

### `Basemap` 节点：

`name` - 在 \[Levels\] 文件夹中 \[level.pak\] 文件的路径（例如: `name="pvp/tdm_farm"`）；

### `TimeOfDay` 节点（可选）：

`file` - 客户端中 TOD 文件的路径（例如: `file="Libs/TimeOfDay/tdm_farm_sunset.tod"`）；

`start` - 日间开始时间，以十进制格式表示；

`end` - 日间结束时间，以十进制格式表示；

`speed` - 日间变化的速度；

### `UI` 节点：

#### `Description` 子节点：

`text` - 地图的英文描述或本地化描述的关键字；

`icon` - 地图图标的名称（图标的名称在 \[/libs/config/ui/mapimagespvp.xml\] 文件中注明，文件中为每个图标提供了路径和尺寸）；

#### `GameMode` 子节点：

`text` - 模式的英文描述或本地化描述的关键字；

### `Sublevels` 节点:

`mission_flow` - 任务执行的类型，对于 PvP 使用 `mission_flow="default"`；

`win_pool` - 胜利时的奖励值；

`lose_pool` - 失败时的奖励值；

`draw_pool` - 平局时的奖励值；

`score_pool` - 奖励值会根据玩家在比赛中获得的分数进行调整，最终值将通过以下公式计算：score_pool \* (player_score / 1stplace_score)，其中 score_pool 是文件中的值，player_score 是玩家的分数，1stplace_score 是第一名玩家的分数。第一名的玩家将获得 score_pool 的最大奖励；

### `TimeDependency` 节点：

`min_time` - 最少时间（以秒为单位），这意味着如果比赛在此时间之前结束，玩家将仅获得文件中指定的最少奖励；

`full_time` - 最大时间（以秒为单位），这意味着如果比赛在此时间之后结束，奖励将不会在 min_time 和 full_time 之间按比例减少；

### `KillDependency` 节点：

`min_kills` - 最少击杀数，这意味着如果整个比赛中的击杀数少于此值，玩家将仅获得最少奖励；

`full_kills` - 最大击杀数，如果整场比赛中的击杀数大于或等于此值，奖励将不会在 min_kills 和 full_kills 之间按比例减少；

### `Objectives` 节点：

在这种情况下，保持为空。

### `Teleports` 节点：

在这种情况下，保持为空。

## 创建 PvE 任务或特别行动的文件

对于 PvE 任务，文件的创建方式略有不同。虽然它仍然包含与 PvP 文件相同的参数，但我将重点说明其中的不同之处。

整体结构：

```xml
<mission name="" time_of_day="" game_mode="pve" game_mode_cfg="pve_mode.cfg" uid="" release_mission="" clan_war_mission="" only_clan_war_mission="" difficulty="" mission_type="" comics_intro="">
  <Basemap name=""/>
  <TimeOfDay file="" start="" end="" speed="" />
  <UI>
    <Description text="" icon=""/>
    <GameMode text=""/>
  </UI>
  <Sublevels>
    <Sublevel id="" name="" mission_flow="" score="" difficulty="" difficulty_cfg="" win_pool="" lose_pool="" draw_pool="" score_pool=""/>
  </Sublevels>
  <Objectives>
    <Objective type="primary" timelimit=""/>
    <Objective type="secondary" completion_score="" id=""/>
  </Objectives>
  <Teleports>
    <Teleport start_sublevel_id="" start_teleport="" finish_sublevel_id="" finish_teleport=""/>
  </Teleports>
</mission>
```

### `mission` 节点：

`difficulty` - 任务的难度（难度类型：easy - 容易；normal - 中等；hard - 困难；survival - 同样困难，但任务只有一种难度）；

`mission_type` - 用于定义奖励乘数，这些乘数将在文件 \[/libs/config/masterserver/rewards_configuration.xml\] 中进行设置；

`comics_intro` - 在界面中播放的漫画的 XML 文件名，存放于 \[ui/comics/\] 文件夹中；

### `Sublevels` 节点：

#### `Sublevel` 节点：

`id` - 子层的编号，从 0 开始计数；

`name` - \[Levels\] 文件夹中 \[submissionconfig.xml\] 文件的路径，该文件中将包含主要奖励参数。创建 \[submissionconfig.xml\] 文件的说明稍后提供，您可以尝试根据客户端现有文件自行创建；

`mission_flow` - 任务的执行类型（"passage" - 通过；"passage_backward" - 反向通过，用于支持此功能的 PvE 任务；"convoy" - 护送；"boss" - boss 战；"arena" - 静态竞技场；"arena_flow" - 动态竞技场）；

`score` - 目前关于分数的用途尚不明确，默认值为 `score="0"`；

`difficulty` - 任务的难度（难度类型：easy - 容易；normal - 中等；hard - 困难；survival - 同样困难，但任务只有一种难度）；

`difficulty_cfg` - 任务难度的 CFG 文件的完整名称（这些文件在客户端中不存在，存储在服务器路径： \[config/content/\] 中）；

`win_pool` - 胜利时的奖励值（可以保持为 `win_pool="0"`，因为该值对结果没有影响）；

`lose_pool` - 失败时的奖励值（可以保持为 `lose_pool="0"`，因为该值对结果没有影响）；

`draw_pool` - 平局时的奖励值（可以保持为 `draw_pool="0"`，因为该值对结果没有影响）；

`score_pool` - 根据玩家在战斗中获得的分数来调整的奖励值（可以保持为 `score_pool="0"`，因为该值对结果没有影响）；

此节点可以有多个实例，具体取决于任务所包含的关卡数量。

### `Objectives` 节点：

#### `Objective` 节点：

`type` - 任务目标的类型（"primary" - 主要目标；"secondary" - 次要目标）；

`timelimit` - 任务的时间限制（以秒为单位），表示任务的最长持续时间，超过该时间任务将以失败告终；

`completion_score` - 完成该目标所需的分数；

`id` - 目标的 ID，需在文件 \[/libs/config/secondaryobjectivesdesc.xml\] 中指定；

### `Teleports` 节点：

#### `Teleport` 节点：

`start_sublevel_id` - 起始任务的编号（来自 `Sublevels/Sublevel` 节点）；

`start_teleport` - 起始传送点的名称，可能在创建关卡时生成（具体不太确定）；

`finish_sublevel_id` - 下一任务的编号（来自 `Sublevels/Sublevel` 节点）；

`finish_teleport` - 终点传送点的名称，可能在创建关卡时生成（具体不太确定）；

# 总结

至此，创建 Warface 服务器启动级别的 XML 文件的过程已完成。您可以为该文件命名任何名称，但最好使用与您的关卡相同的名称（如果您有任务，则使用任务名称和其难度）。该文件应位于路径 \[/libs/missions/\] 下。现在，您的地图或任务已准备好在游戏中全面使用！
