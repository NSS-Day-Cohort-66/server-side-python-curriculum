# Writing the `update` Requests

The `update` method will handle the `PUT` requests to the resource. In this chapter, we’ll add the `update` method to the `GameView` and `EventView`.

## Learning Objectives

* You should be able to explain which HTTP method is used by the client to trigger an update request.
* You should be able to identify which method on a ViewSet is invoked when the client has requested a change in state for a resource.

## API View Code

`PUT` requests expect the entire object to be sent to the server regardless of whether a field has been updated. Here is the `update` method for the `GameView`:

```python
def update(self, request, pk):
    """Handle PUT requests for a game

    Returns:
        Response -- Empty body with 204 status code
    """

    # Use the ORM to get the requested game from the DB

    # Use the ORM to get the correct instance of the assigned game type

    # Update all properties with the values from the request payload


    # Save the updated game
    game.save()

    return Response(None, status=status.HTTP_204_NO_CONTENT)
```

Just like in the `retrieve` method, we grab the `Game` object we want from the database. Each of the next lines are setting the fields on `game` to the values coming from the client, like in the `create` method. After all the fields are set, the changes are saved to the database.

### Postman

The `update` method is called when any `PUT` requests are made to `http://localhost:8000/games/{game_id}` Find the `id` for the “Codenames” game and send a `PUT` request for that game id. Let’s update the `title` and `numberOfPlayers`. Here’s the body to use in postman for the request:

Again, send the properties that you defined on your model.

```json
{
    "title": "Codenames 2 Player",
    "maker": "CGE",
    "number_of_players": 2,
    "skill_level": 3,
    "game_type": 2
}
```
After making the request, `retrieve` the game to verify the updates

## On Your Own
Write the code to `update` an event
