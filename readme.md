# Deploy Command Basics

A small project about turning a repeated deploy flow into a command I can run from anywhere in session.

The main idea:

```text
executable file → folder in PATH → command available anywhere
```

---

## Why

I often end up running several commands in order, so I wanted one command that runs the full sequence for me.

I can just run:

```bash
deploy-example
```

---

## Starting point

First, create a `bin` directory inside the current user's home directory:

```bash
mkdir -p ~/bin
```

From here, create the command file:

```bash
nano ~/bin/deploy-example
```

Example file contents:

```bash
#!/usr/bin/env bash

echo "Deploy command works"
```
Here you can run dependency installation, migration and build files within a single executable file that you can call with a single cammand.

Next, give the file executable permission:

```bash
chmod u+x ~/bin/deploy-example
```

We need to be able to run the executable file so we are adding permissiion to user/owner.

Now check what is currently included in `PATH`:

```bash
echo $PATH
```

If the user `bin` directory is not included, add it to the bottom of `~/.profile`:

```bash
nano ~/.profile
```

Add this line:

```bash
export PATH="$HOME/bin:$PATH"
```
We are essentially setting the new PATH variable to include our folder as first search dir. Make sure its unique

Reload the profile file without restarting the session:

```bash
source ~/.profile
```

Now check `PATH` again:

```bash
echo $PATH
```

You should see your user `bin` directory included.

Now the command can be run from anywhere:

```bash
deploy-example
```

---

## What this shows

At its simplest a terminal command, can just be an executable file in a location the shell knows how to search.

In this case:

```text
deploy-example file
↓
made executable
↓
placed in ~/bin
↓
found through PATH
↓
run like a normal command
```

---

## Next

This still requires manually running the command on the server.

The next step would be moving the same deploy flow into a GitHub Actions pipeline.
