# Listing Games and Events in the Client
Now that we’ve added a way to get all games and events from the server, let’s display those lists in React.

## Client Code

You can start off with this starter React code to request and display a list of games from the API. Fill in the blanks.


> #### `src/components/game/GameList.js`

```jsx
import React, { useEffect, useState } from "react"
import { getGames } from "../../managers/GameManager.js"

export const GameList = (props) => {
    // Establish the state
    const [ games, setGames ] = useState([])

    // Get the state after initialization
    useEffect()

    return (
        <article className="games">
            {
                // Render the state
            }
        </article>
    )
}
```

> #### `src/views/ApplicationViews.js`

```jsx
import { Route, Routes } from "react-router-dom"
import { Login } from "../components/auth/Login"
import { Register } from "../components/auth/Register"
import { Authorized } from "./Authorized"
import { GameList } from "../components/game/GameList"


export const ApplicationViews = () => {
    return <>
        <Routes>
            <Route path="/login" element={<Login />} />
            <Route path="/register" element={<Register />} />
            <Route element={<Authorized />}>
                <Route path="/" element={<GameList />} />
            </Route>
        </Routes>
    </>
}
```

## Practice: Listing Events

Create your component(s) and route needed to display a list of events. The route should be `/events` for the event list.
