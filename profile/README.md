# Serviceportal

## Hi there 👋

## Installation

## Docker (lokal)

### Windows (PowerShell)

```powershell
docker run --hostname=serviceportal.example.ch --name "serviceportal-local" `
    --env=NODE_ENV=development `
    --env=DB_HOST="dbhost.example.ch" `
    --env=DB_NAME="db_ssp" `
    --env=DB_PASS="**********" `
    --network=bridge -p 8080:80 `
    --restart=no `
    --runtime=runc -d `
    mrs:deb12-602121
``` 

## Front-end (Templates)

1. `cd /var/www/`
2. `git clone git@github-serviceportal:serviceportal-dev/html.git`

## Backend (Controller)

1. `cd /usr/local/lib/site_perl`
2. `git clone git@github-modules:serviceportal-dev/ScreenPoint.git`
3. `git clone git@github-autoload:serviceportal-dev/auto.git`

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
