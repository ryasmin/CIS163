## Fix the Method Types
You are building a small game engine.

Some methods are incorrectly defined as instance methods, static methods, or class methods.

Your task is to:
- Identify which methods are incorrectly defined.
- Modify each method to use the correct decorator.

```
class GameConfig:
    max_players = 4
    bonus_multiplier = 1.0
  
    def set_max_players(n):
        GameConfig.max_players = n

    def validate_player_count(count):
        return count <= GameConfig.max_players

    def apply_bonus(score):
        return int(score * GameConfig.bonus_multiplier)


class ProGameConfig(GameConfig):
    max_players = 8
    bonus_multiplier = 1.5


class Player:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def from_string(data):
        name, score = data.split(":")
        return Player(name, int(score))

    def reset_score():
        self.score = 0

    def add_points(self, pts):
        self.score += ProGameConfig.apply_bonus(pts)


class Tournament:
    def __init__(self, players, config):
        self.players = players
        self.config = config

    def create_empty():
        return Tournament([], GameConfig)

    def add_player(self, player):
        if self.config.validate_player_count(len(self.players) + 1):
            self.players.append(player)

    def total_score():
        return sum(p.score for p in self.players)
```
