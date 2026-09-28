# battlecode

Our bot for UNSW Battlecode. The bot is `mybot/main.py`. That's basically the only file we edit.
quickstart: https://game.battlecode.au/docs/quickstart
api key (used for terminal submission): our team page on the battlecode website

## setup (once)

```
git clone https://github.com/Jiji-courier/battlecode-O-no--2026
pip install unswbc
```

## running a game

```
unswbc run maps/default.map mybot mybot
```

That makes a `.replay` file in `replays/`. Click it in VS Code, or open it in the visualiser on the site.

## workflow

**pull → edit → test → commit → push → submit**

1. **pull first**: Run `git pull`
2. edit `mybot/main.py`
3. **test it against the old version** before pushing (see below). Don't push something that loses
4. commit with a message that says what changed
5. push

Everyone works on `main`and keep commits small and push often so conflicts are rare and tiny.

### big experiments

However, if you're trying something that might not work out (rewriting movement, sonar, portals...), make a branch named after the idea:

```
git checkout -b sonar-test
```

If it wins, merge it into main.

## testing a change

Save the current bot in `bots/` before you change it, then play old vs new:

```
cp -r mybot bots/v1
unswbc run maps/default.map mybot bots/v1
```

Try a few maps (`maps/` has lots), and swap the order too, since being team A vs team B can matter.

## submitting

1. make sure you've **committed and pushed** first
2. get the commit id:
   ```
   git rev-parse --short HEAD
   ```
3. upload on the Submissions page (language Python, zip of `main.py`, `helper.py` and `bot.toml`), or run the following in your terminal (api key on our team page):
   ```
   unswbc auth set <api key>
   unswbc submit mybot -n <name> -d "<commit id> <what changed>"
   ```

- **name** = short and readable, e.g. `split-at-10`
- **description** = the commit id (+ the message if you want)

Why the id and not just the message: the id points to exactly one version of the code, so we can always tell which code is running. To look at that code later, go to `https://github.com/Jiji-courier/battlecode-O-no--2026/commit/<id>`.

## don't

- don't commit your API key (`bc_...`). `unswbc auth set` already keeps it outside the repo
- don't commit replays or zips (they're in `.gitignore`)
- don't submit code that isn't pushed