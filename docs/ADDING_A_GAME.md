# Adding a New Game to GameVault

This guide explains how to add a new game to GameVault. Follow the steps below to create the game component, register it, and display it in the game catalog.

## 1. Set Up the Project

Make sure you have Node.js and npm installed.

Clone the repository and open the project folder:

```bash
git clone https://github.com/Aaqibhafeezkhan/GameVault.git
cd GameVault
```

Install the project dependencies:

```bash
npm ci
```

Start the development server:

```bash
npm run dev
```

Open the local URL shown in your terminal to view the application.

## 2. Create the Game Component

Game components are stored inside:

```text
src/games/
```

Create a new folder for your game. For example:

```text
src/games/MyGame/
```

Inside this folder, create an `index.jsx` file:

```text
src/games/MyGame/index.jsx
```

Your game component should be a React component with a default export.

For example:

```jsx
function MyGame() {
  return (
    <div>
      <h2>My Game</h2>
      <p>Welcome to my game!</p>
    </div>
  );
}

export default MyGame;
```

You can add your game's logic, styling, and other required functionality inside this component.

## 3. Register the Game Component

Open:

```text
src/App.jsx
```

Find the `GameComponents` object. It contains the game slugs and their corresponding lazy-loaded components.

Add an entry for your game:

```jsx
"my-game": lazy(() => import("./games/MyGame")),
```

Make sure the import path matches your game folder and the slug matches the metadata entry you will add in the next step.

## 4. Add Game Information

Open:

```text
src/data/gamesData.js
```

Find the `gamesData` array and add a new game object.

Each game entry should contain these five fields:

| Field | Description |
|---|---|
| `slug` | Unique URL-friendly identifier for the game |
| `title` | Name displayed to users |
| `category` | Category of the game |
| `difficulty` | Difficulty level |
| `description` | Short explanation of the game |

Example:

```js
{
  slug: "my-game",
  title: "My Game",
  category: "Strategy",
  difficulty: "Easy",
  description: "A short description of my game."
}
```

Use a unique slug and make sure it matches the key added to `GameComponents` in `src/App.jsx`.

## 5. Understand the Shared Game Layout

GameVault uses a shared `GameShell` component to display games.

The `GameRoute` function in `src/App.jsx` wraps each game component inside `GameShell` and passes the game's title.

You do not need to add another `GameShell` inside your game component. Focus on implementing the game itself.

## 6. How Game Routes Work

GameVault uses `HashRouter` and generates game routes from the `gamesData` array in `src/App.jsx`.

For each game, the application creates a route using its slug:

```text
/game/my-game
```

The application uses that same slug to find the corresponding component in `GameComponents`.

This is why the slug in both places must match.

## 7. Verify Your Game

After adding the component and metadata:

1. Run the development server using `npm run dev`.
2. Open the application in your browser.
3. Check that your game appears in the game catalog.
4. Select the game and confirm that it launches correctly.
5. Check that the game title and shared layout display properly.
6. Check the browser console for errors.

## 8. Build the Project

Before submitting your changes, run:

```bash
npm run build
```

Make sure the production build completes successfully.

## 9. Submit Your Contribution

Create a new Git branch for your changes:

```bash
git switch -c feat/add-my-game
```

Commit your changes and push the branch:

```bash
git add .
git commit -m "feat: add my game"
git push -u origin feat/add-my-game
```

Then open a pull request against the repository's `main` branch and describe the changes you made.

Happy contributing!