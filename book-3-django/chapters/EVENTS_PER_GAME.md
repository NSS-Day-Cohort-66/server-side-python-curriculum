# SQL Aggregation in Django ORM

In SQL, you can use functions like MIN(), MAX(), AVG(), and COUNT() to perform operations on multiple rows of a particular column and result in a single value.

Here's a simple example with games and events.

## Events Per Game in SQL

Consider the following, simplified table containing games.

> #### Games

| id | title | skill_level |
|--|--|--|
| 1 | Risk | 2 |
| 2 | Clue | 4 |
| 3 | Stratego | 3 |

Here is a table that records events. There are 3 events for Risk, 2 events for Clue, and 3 events for Stratego.

> #### Events

| id | date | game_id |
|--|--|--|
| 1 | 2020-12-20 | 1 |
| 2 | 2020-11-19 | 1 |
| 4 | 2020-11-03 | 1 |
| 5 | 2021-01-05 | 2 |
| 6 | 2020-11-19 | 2 |
| 7 | 2021-01-09 | 3 |
| 8 | 2021-02-11 | 3 |
| 9 | 2020-11-16 | 3 |

#### Events per Game SQL

To find the number of events per game, you would write the following SQL. One thing to remember is that every time you perform an aggregation operation in SQL, you must have a `GROUP BY` clause in your statement.

```sql
SELECT
    g.title,
    COUNT(e.id) event_count
FROM Games g
    JOIN Events e ON e.game_id = g.id
GROUP BY g.title
```

It would provide the following result set.

| title | event_count |
|--|--|
| Risk | 3 |
| Clue | 2 |
| Stratego | 3 |

## Events per Game with Django

### Models

Make sure the `game` field on the event has a `related_name` attribute. This sets up an `events` field on the `game` that holds a list of the `events` that the `game` is attached to. 

```py

class Event(models.Model):

    date = models.DateField(auto_now=False, auto_now_add=False)
    game = models.ForeignKey(Game, on_delete=models.CASCADE, related_name='events')
```


### Annotate with Count

In Django, you can use the `annotate` property with the `Count()` method to perform the same operation.

First, make sure you import the Count method.

```py
from django.db.models import Count
```

Then, in your `list` method on the game ViewSet, you can put the following code.

```py
games = Game.objects.annotate(event_count=Count('events'))
```

This statement will produce the exact same SQL statement as the one you wrote above and give you the same results.

The last step would be to make sure that `event_count` got serialized in order to be sent back to the client as a property in the JSON. Since `event_count` is not a field on the model, we'll need to tell the serializer to expect a new field to sometimes be passed to the serializer

```py
class GameSerializer(serializers.ModelSerializer):
    event_count = serializers.IntegerField(default=None)

    """JSON serializer for games"""
    class Meta:
        model = Game
        fields = ('all the other fields you already have', 'event_count')
```

Then the client would receive the following JSON.

```json
[
    {
        "id": 1,
        "title": "Risk",
        "event_count": 3
    },
    {
        "id": 2,
        "title": "Clue",
        "event_count": 2
    },
    {
        "id": 3,
        "title": "Stratego",
        "event_count": 3
    }
]
```
