# Writing the `create` method
The `create` method will handle the `POST` requests to the resource. In this chapter, we’ll add the `create` method to the `GameView` and `EventView`.

## Create a Game
Before writing the create code, take a look back at the `Game` model. We’ll need values from the client for all of the fields on the model.
Here’s the code to create a game. We’ll break it down next.

```py
def create(self, request):
    """Handle POST operations

    Returns
        Response -- JSON serialized game instance
    """
    game_type = GameType.objects.get(pk=request.data["game_type"])

    # Use the create() method shortcut or the imperative approach.
    # Whichever appeals to you.

    # Serialize the data and send it back to the client
```

### Try it in Postman

Since we’ve added the `create` method to the view class, the `router` inside of `urls.py` already knows that this will be an acceptable route to hit. All `POST` calls to `http://localhost:8000/games` will now call the `create` method. Open up Postman to try it out. Add this game to the request body:

If you did not add all of these fields to your **Game** model, that's fine. Modify this JSON to match which fields you defined.

```json
{
    "title": "Codenames",
    "maker": "CGE",
    "number_of_players": 6,
    "skill_level": 3,
    "game_type": 2
}
```

## On Your Own

Add the `create` method to the `EventView`. Take a look at the `Event` model to remember which fields you’ll need to account for. For now, don't add any `attendees` to the event. We'll look at adding that later. By the end, a `POST` request to `http://localhost:8000/events` should add a new event to the database.
