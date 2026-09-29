# GAR Starter

An empty MonoGame game, set up with the content builder. Use it to start your own game in
the Game Architecture course.

## Getting started

1. On GitHub, click **Use this template** → **Create a new repository**, then clone your new
   repository.
2. Run the game:

   ```
   dotnet run --project MyGame
   ```

   You should see an empty cornflower-blue window. Press `Esc` to quit.

Open `MyGame.slnx` in Visual Studio or Rider, or the folder in VS Code.

## Layout

| Path | What it is |
| --- | --- |
| `MyGame/` | Your game. `Game1.cs` is where it starts. |
| `GARCore/` | The course's core library: code any game could reuse. Empty to begin with. |
| `Content/Assets/` | Your raw assets: images, fonts, sounds, music, data files. |
| `Content/Builder/Builder.cs` | The rules for how each kind of asset is built. |

## Adding assets

Put the file in `Content/Assets` (subfolders are fine) and load it by its path, without
the extension:

```csharp
// Content/Assets/images/player.png
Texture2D player = Content.Load<Texture2D>("images/player");
```

The builder runs automatically every time the game builds. It already handles `.png`,
`.spritefont`, `.wav` and `.mp3`, and copies `.json` and `.xml` files as they are (read
those yourself from `Content/...` at runtime). For any other kind of file, add a rule in
`Builder.cs`.

If you replace a font's `.ttf`, also save its `.spritefont` (or delete `MyGame/obj`): the
content builder only rebuilds a font when the `.spritefont` itself changes.

## Renaming the game

To give the project your game's name (e.g. `Frogger`):

1. Rename the `MyGame` folder and `MyGame.csproj` to `Frogger` and `Frogger.csproj`.
2. Replace `MyGame` with `Frogger` in `MyGame.slnx` (then rename it too), `Program.cs`
   and `Game1.cs`.

## GARCore

`GARCore` is a class library: code that isn't specific to one game, kept apart so any game
can reuse it. It starts empty. The game references it in `MyGame.csproj`:

```xml
<ProjectReference Include="..\GARCore\GARCore.csproj" />
```

The reference only goes one way. The game uses `GARCore`, but nothing in `GARCore` may use
a class from `MyGame`; otherwise no other game could reuse it.

In the course you build `GARCore` up session by session. To use the course's version in
your own game, replace this `GARCore` folder with the one from a game in
[gar-games](https://github.com/Metamate/gar-games), usually the latest game you've covered.
Nothing else needs to change. If your game doesn't use it, you can leave it empty.

## Publishing

```
dotnet publish MyGame -c Release -r win-x64 --self-contained
```

Use `osx-arm64` or `linux-x64` for other platforms. The game and its `Content` folder
end up in `MyGame/bin/Release/net10.0/win-x64/publish`.
