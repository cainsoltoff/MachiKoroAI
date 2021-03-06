# Machi Koro by Cain Soltoff

I recently played Machi Koro for the first time with some friends.  Given the relative simplicity, it seemed like the perfect game on which to train a deep neural net, so that's what I'm working on!
<br>
<br>
For now, I implemented a customizable version of the base game in Python.  You can play with human players, use AI that make random choices, or make your own player agents. 


<b>Machi Koro Module and Implementation Details</b>
---

The MachiKoro package contains all the necessary code to play the game with humans, AI players, or your own subclassed PlayerControllers. Currently, only the original game is implemented, but I will eventually add the expansions.  You can  customize many details of the game including the card set, card details like payouts/payout conditions/dice triggers/names, and intial game values (like the initial cards or initial coins per player).  This is done by changing the CSV files in the module and calling reloadDB in *MachiKoro.StaticCardDatabase*.

<b>MachiKoro.GameController</b> - This is the main sub-module which contains the main GameController.
                           

<b>MachiKoro.PlayerController</b> - Contains an abstract base class Player Controller that can be sub-classed to create new player controllers.
                             Also includes two player controller types - a randomized AI and a human player (where the game queries the player for input).
                             Add PlayerControllers to the GameController via the latter's add_player_controller method.

<b>MachiKoro.StaticCardDatabase</b> - generates a serialized python object *static_game_db.pkl* (if it doesn't exist) containing all the base game information on cards
                                      and players (through the csv files in csv_game_db_files).  There's also a top-level reloadDB method that forces the regeneration of the .pkl file from
                                      the underlying CSV files (i.e. call if you make edits to the csv files).


---
<b>*Example: Three Player Game with One Human and Two AI's*</b>




```
from MachiKoro.GameController import GameController
from MachiKoro.PlayerController import RandomAIPlayerController, HumanPlayerController

game = GameController(num_players=3, print_actions=False)

game.add_player_controller(HumanPlayerController(game))
game.add_player_controller(RandomAIPlayerController(game))
game.add_player_controller(RandomAIPlayerController(game))

game.run_game()

```
