# Elixir Chat App Fixes

These are some fixes to get the chat app working on the RPi. You might not need all of these fixes.

## Upgrading Elixir

I had to upgrade Elixir to 1.4 (from 1.3.3). I first had to remove the current installations of erlang and elixir from the RPi

Removing Erlang and Elixir
```bash
sudo apt-get remove erlang
sudo apt-get remove erlang-dev
sudo apt-get remove elixir
```

[Reinstalling Erlang and Elixir](https://elixir-lang.org/install.html)
```bash
echo "deb https://packages.erlang-solutions.com/debian stretch contrib" | sudo tee /etc/apt/sources.list.d/erlang-solutions.list
```
```bash
wget https://packages.erlang-solutions.com/debian/erlang_solutions.asc
sudo apt-key add erlang_solutions.asc
```
```bash
sudo apt update
sudo apt install elixir
```
```bash
sudo ln -s /usr/local/bin/iex /usr/bin/iex
sudo ln -s /usr/local/bin/mix /usr/bin/mix
```

## Installing Node.js
[Install Guide](https://www.w3schools.com/nodejs/nodejs_raspberrypi.asp)
```bash
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
```
```bash
sudo apt-get install -y nodejs
```

## Installing Postgres
[Install Guide](https://opensource.com/article/17/10/set-postgres-database-your-raspberry-pi)

```bash
sudo apt install postgresql libpq-dev postgresql-client postgresql-client-common -y
```
```bash
sudo su postgres
createuser pi -P --interactive
```
When prompted, enter a password (and remember what it is), select n for superuser, and y for the next two questions.

## Phoenix Installation
[Install Guide](https://hexdocs.pm/phoenix/installation.html)

```bash
mix local.hex
mix archive.install hex phx_new 1.4.0
```
```bash
mix phx.new app
cd app/
npm install
```

#### Config Changes
```ex
# /config/dev.exs
# Line 52
username: "pi",

#Line 53
password: [The password you setup in the Postgres install],
```

# The Rest of the Chat App Guide

[Guide](https://work.stevegrossi.com/2016/07/11/building-a-chat-app-with-elixir-and-phoenix-presence/)

Use this command to setup the app
```bash
mix ecto.create
```
Use this command to run the server when needed
```bash
mix phx.server
```

You can then follow the rest of the guide starting with the section that begins with

> This default page corresponds to the web/templates/pages/index.html.eex template file

[You can also use the GitHub repo to guide your code](https://github.com/stevegrossi/phoenix_chat/tree/chat)
