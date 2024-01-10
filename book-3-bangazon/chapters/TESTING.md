# Creating API Integration Tests

## Learning Objective

After implementing the code in this chapter, you should be able to understand the purpose of an integration test, and be able to apply code that verifies that API operations perform the tasks that you expect.

## Process to Follow

When you want to have a test suite that verifies that your code continues to work as developers make changes, here's the quick list of things you need to

1. Create `tests` directory in project.
2. Create `tests/__init__.py` module.
3. Create `tests/{resource_name}_tests.py` module for each resource.
4. Write test classes in each test module.
5. Import test classes into `__init__.py`.
6. Run `python3 manage.py test tests -v 1` to execute all test classes.

## Summary

Time to get meta. Integration tests are a separate application that you write whose sole job is to verify that the implementation code does what it's supposed to do. This is important in a large project where there are many developers all working on big fixes and new features.

The integration tests ensure that as bugs are fixed, and new features are built, that teammates do not break existing functionality.

The entire team works on designing the integration tests and agree that when a certain endpoint is requested, with a certain HTTP method, that the end result should be _x_. Then the test is written to check if _x_ is achieved when a request is made.

Remember that humans are extraordinarily adept at introducing unintended bugs into a codebase while development is happening. The integration tests serve as a neutral third-party to ensure that those bugs don't make it to production.

## Implementation Code

### Package Init Module

Just like with your views and models in your API application, your `tests` directory should be made into a Python package by implementing a dunder-init module.

> #### `levelup/tests/__init__.py`

```py
from .game_tests import GameTests
```

### Test Case(s) Module

Now create the module that contains the first integration test.

1. For each resource you want to test (e.g. games, events, etc.) there will be a class. In this module, the `GameTests` class will contain all integration tests for games.
1. If you need to have any resources created *before* a test is run, you can do that in `setUp()`. In the code below, the set up function does two things:
    1. Registers a user in the testing database.
    1. Seeds the testing database with a game type
1. Then define functions for running the integration tests. All functions that contain integration tests **must** start with `test_`. What you put after that is up to you. Just make sure it is very descriptive. If the test is for modifying a game, then a good name for that function would be `test_modifying_a_game_record_via_put_method()`.

> #### `levelup/tests/game_tests.py`

```py
import json
from rest_framework import status
from rest_framework.test import APITestCase
from levelupapi.models import GameType, Gamer
from rest_framework.authtoken.models import Token


class GameTests(APITestCase):

    # Add any fixtures you want to run to build the test database
    fixtures = ['users', 'tokens', 'gamers', 'game_types', 'games', 'events']

    def setUp(self):
        self.gamer = Gamer.objects.first()
        token = Token.objects.get(user=self.gamer.user)
        self.client.credentials(HTTP_AUTHORIZATION=f"Token {token.key}")

    def test_create_game(self):
        """
        Ensure we can create a new game.
        """
        # Define the endpoint in the API to which
        # the request will be sent
        url = "/games"

        # Define the request body
        data = {
            "gameTypeId": 1,
            "skillLevel": 5,
            "title": "Clue",
            "maker": "Milton Bradley",
            "numberOfPlayers": 6,
        }

        # Initiate request and store response
        response = self.client.post(url, data, format='json')

        # Parse the JSON in the response body
        json_response = json.loads(response.content)

        # Assert that the game was created
        self.assertEqual(response.status_code, status.HTTP_201_CREATED)

        # Assert that the properties on the created resource are correct
        self.assertEqual(json_response["title"], "Clue")
        self.assertEqual(json_response["maker"], "Milton Bradley")
        self.assertEqual(json_response["skill_level"], 5)
        self.assertEqual(json_response["number_of_players"], 6)
```

## Running the Test

1. Open a terminal and change directory to your project directory.
1. Run the following command
    ```sh
    python3 manage.py test tests -v 1
    ```
1. Look at the output and see if the test passes.
    ![expected test output in terminal](./images/initial-test-output.png)
1. If your test passed, move on to the next section, otherwise, call in an instructor.

## Testing GET

```py
    def test_get_game(self):
        """
        Ensure we can get an existing game.
        """

        # Seed the database with a game
        game = Game()
        game.gametype_id = 1
        game.skill_level = 5
        game.title = "Monopoly"
        game.maker = "Milton Bradley"
        game.number_of_players = 4
        game.gamer_id = 1

        game.save()

        # Initiate request and store response
        response = self.client.get(f"/games/{game.id}")

        # Parse the JSON in the response body
        json_response = json.loads(response.content)

        # Assert that the game was retrieved
        self.assertEqual(response.status_code, status.HTTP_200_OK)

        # Assert that the values are correct
        self.assertEqual(json_response["title"], "Monopoly")
        self.assertEqual(json_response["maker"], "Milton Bradley")
        self.assertEqual(json_response["skill_level"], 5)
        self.assertEqual(json_response["number_of_players"], 4)
```

## Testing PUT

```py
    def test_change_game(self):
        """
        Ensure we can change an existing game.
        """
        game = Game()
        game.gametype_id = 1
        game.skill_level = 5
        game.title = "Sorry"
        game.maker = "Milton Bradley"
        game.number_of_players = 4
        game.gamer_id = 1
        game.save()

        # DEFINE NEW PROPERTIES FOR GAME
        data = {
            "gameTypeId": 1,
            "skillLevel": 2,
            "title": "Sorry",
            "maker": "Hasbro",
            "numberOfPlayers": 4
        }

        response = self.client.put(f"/games/{game.id}", data, format="json")
        self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)

        # GET game again to verify changes were made
        response = self.client.get(f"/games/{game.id}")
        json_response = json.loads(response.content)

        # Assert that the properties are correct
        self.assertEqual(response.status_code, status.HTTP_200_OK)
        self.assertEqual(json_response["title"], "Sorry")
        self.assertEqual(json_response["maker"], "Hasbro")
        self.assertEqual(json_response["skill_level"], 2)
        self.assertEqual(json_response["number_of_players"], 4)
```


## Testing DELETE

```py
    def test_delete_game(self):
        """
        Ensure we can delete an existing game.
        """
        game = Game()
        game.gametype_id = 1
        game.skill_level = 5
        game.title = "Sorry"
        game.maker = "Milton Bradley"
        game.number_of_players = 4
        game.gamer_id = 1
        game.save()

        # DELETE the game you just created
        response = self.client.delete(f"/games/{game.id}")
        self.assertEqual(response.status_code, status.HTTP_204_NO_CONTENT)

        # GET the game again to verify you get a 404 response
        response = self.client.get(f"/games/{game.id}")
        self.assertEqual(response.status_code, status.HTTP_404_NOT_FOUND)
```