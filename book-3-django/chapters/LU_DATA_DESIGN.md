# Karen's Level Up Requirements

## Meeting Karen

> Karen is sitting at the table by the front window of the Cat Café where she wanted to meet and discuss the "program" she wants you to write for her.
>
> She has a grey cat sitting in her lap, which she gently holds in one arm as she takes a sip of her coffee
>
> You greet her and say, "It's a pleasure to meet you, Karen. What a lovely cat!"
>
> She replies, "I'm glad to meet you, too. This is Gentry. He needed some attention this morning, so I decided to bring him with me." She starts to pet his back and tail with her hand.
>
> You eagerly say, "I'm excited to hear what you want me to build for you. I enjoy playing games, too. Mostly video games."
>
> Karen tilts her head slightly, "I've tried a couple of those but haven't gotten the hang of it. What I'm looking for is a way for people to gather and play card games and board games."
>
> "My cat, Sheen," she continues, "likes to play games with me, but nothing quite as complex as Settlers of Catan or Bridge." Her face brightens a bit as she talks about how she tries to get her cats to play games with her.
>
> "One time, I even put catnip on some checkers and tried to see if Checkers, my other cat, could move the piece to play with me. It didn't really work." She laughs lightly, obviously playing the scenario out in her mind.
>
> You also laugh at the idea of a cat playing checkers, and ask, "Can you tell me what you're looking for in the application you want me to build for you?"
>
> "Of course, dear!"
>
> You take your pen out and open your notebook ready to furiously scribble notes.
>
> "I want a way to schedule events for people to play games."
>
> You make a quick note, and then look up at her expectantly, waiting for more information.
>
> Karen smiles a bit, and blinks, thinking she gave you all the information you need.
>
> "Um, ok. Well... what games can people make events for? Any game?"
>
> "I was thinking card games and board games," she replies.
>
> You press on with, "But any one of those games, right?"
>
> "Well, of course, dear. I'm not against learning a new game. As long as I'm meeting people and having fun."
>
> Realizing the client doesn't quite know how to describe how the app will work, you ask some more questions, "Ok, so people can create any game they want. Got it. So... who schedules an event? The person who creates the game, or anyone who wants to play the game?"
>
> Karen looks to the side for a moment to think and replies, "I think anyone should be able to schedule an event for any game that has been added."
>
> You write more notes.
>
> "Oh!" she exclaims quickly, "and I want people to say if they are coming. That way the person holding the event knows how many people to expect. It's only proper."
>
> You ask, "And anyone can sign up for any event?"
>
> "The more the merrier, dear." She looks down at Gentry, and continues, "Just like with my cats. The more the merrier."
>
> You finish writing your notes, smile, and say, "I think I have all I need to get an initial version for you to see and give me feedback. It was so lovely to meet you, Karen."
>
> She stands with Gentry, and replies, "Lovely to meet you as well. I can't wait to share it with my knitting and book clubs. We've all been trying to branch out a little."
>
> You reply, "That's great! I'll let you know when I'm done with the first version and we can schedule a time to meet again."
>


## Learning Objectives

* You should be able to create an ERD based on verbal requirements from a non-technical customer.
* You should be able to design a Django database model class based on the table definition in your ERD.
* You should be able to explain the process of using Django commands to get your models turned into database tables.
* You should be able to predict how a database table should be structured given a Django model.
* You should be able to clarify the difference between a one-to-many relationship and a one-to-one relationship.



## ERD

* There will be 5 main tables used for this application
  1. **User**
  1. **Game**
  1. **GameType**
  1. **Event**
  2. **EventGamer**
* The **User** table we get for free, so you just need to import it.
* The **Game** table will have a one to many relationship with **GameType** since a game will be associated with 1 game type and a game type can be associated with many games.
* The **Game** table will also have a one to many relationship with **User** because gamers can create more than one game.
* The **Event** table will have a 1 to many relationship with **User**, called the organizer, because gamers can host many events but an event will only have 1 host.
* When a gamer wants to attend an event, you need to store that relationship. Since this is a many to many relationship, they will be stored in **EventGamer**.

Given these requirements, design an accurate ERD for the database.

## Resources
* [Django Models](https://docs.djangoproject.com/en/3.2/topics/db/models/) - Overview of Django Models
* [Extending the User Model](https://docs.djangoproject.com/en/dev/topics/auth/customizing/#extending-the-existing-user-model) - Explanation for how to add fields to the Django user
* [Model Field Types](https://docs.djangoproject.com/en/3.2/ref/models/fields/#field-types) - All the options for data types in a model
* [One to Many Relationships](https://docs.djangoproject.com/en/3.2/topics/db/models/#many-to-one-relationships) - How to add a foreign key to a model
* [Many to Many Relationships](https://docs.djangoproject.com/en/3.2/topics/db/models/#many-to-many-relationships) - How to set up a Many-Many Relationship

## Level Up Models

Once you have looked over the ERD and understand relationships for users, games, and event create your model modules and classes. Then import the classes into the package init module.

## Migration of Models

__Once you have defined your models, you should review them with an instructor.__

When your models are approved, you can then create a migration to create the tables in your database.

```sh
python3 manage.py makemigrations levelupapi
```

Now that migrations are created, run the following command to execute your migrations and create the tables in your database.

```sh
python3 manage.py migrate
```

You should now have a `db.sqlite3` file in the project folder.
