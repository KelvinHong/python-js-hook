# Add JavaScript code formatter to your (mainly) Python project

## TL; DR

If you prefer to use `pre-commit` hook, go to `.pre-commit-config.yaml`, add the following `prettier`
hook to format your javascript code.

```yml
repos:
  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v3.1.0
    hooks:
      - id: prettier
```

## Main thread

I built a full-stack project that uses Python as backend and React JS as frontend, while I'm quite familiar with all the
`pre-commit` hooks in Python, I was finding something similar for javascript.

Previously I tried `ESLint` without thinking about what it actually does. then I learned about the difference of a linter and
code formatter! And what I found out is that `ESLint` is not actually a code formatter.

When using the `black` `pre-commit` hook, everytime I commit my code, there is a high chance that `black` will reject my code because
it doesn't follow a strict format, and that is good, because my code are often messy or I don't care much about the beauty of my code
(which is something I should take greater care of!).

Often time my workflow become something like this:

```console
git add main.py
git commit -m "feat: Add some new feature" # black reject
git add main.py # Simply run this again
git commit -m "feat: Add some new feature" # Finally pass.
```

So I regard this as "aggresive" formatter because it not only tell me where is the issue, but also fix it for me.
In fact, the `isort` hook also does similar thing, just that it sorts Python imports in some pre-defined order.
I think this is a very good feature and make the code adhere to a certain quality.

However, when I initially add the frontend to my project, I struggled to find a good code formatter (where I don't even know I want a
code formatter at that time). With the time constraint from my work, I hastily slaps the `ESLint` into my pre commit hooks and
called it a day.

While sometimes `ESLint` works, it didn't even once modify my code, but just tell me what I can do to make my code better
(again, I'm not very clear about the difference between linter and formatter at the time).
I tried purposefully type some javascripts with very bad aesthetic but it still didn't change my code.

That is, until today I found out we can use `prettier` to format my javascript code.
Reading the [Prettier documentations](https://prettier.io/docs/en/precommit.html), we can add the `prettier` hook into `.pre-commit-config.yaml`
like so:

```yml
- repo: https://github.com/pre-commit/mirrors-prettier
  rev: v.3.1.0
  hooks:
    - id: prettier
```

I chosed `v3.1.0` because it is the last stable release before all of the `v4 alpha` builds, not to mention
it is good enough for my work.

Now I have `index.js`, and when I purposefully make it looks bad:

```js
function main() {
  console.log("Hello World!");
}

export default main;
```

After running `git add` and `git commit`, the commit failed with the `index.js` file changed to

```js
function main() {
  console.log("Hello World!");
}

export default main;
```

Which is exactly what I wanted!
I will then `git add` and `git commit` again, it passed, then continue my work.
