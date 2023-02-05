# Growthbook & Monk

This repository contains Monk.io template to deploy Growthbook & Monk either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

### Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository

```bash
git clone https://github.com/monk-io/growthbook
```

## Load Template

```bash
cd growthbook
monk load MANIFEST
```

### Let's take a look at the themes I have installed

```bash
foo@bar:~$ monk list growthbook
✔ Got the list
Type      Template                       Repository  Version  Tags
runnable  growthbook/growthbook     local       -        -
runnable  growthbook/growthbook-db  local       -        -
group     growthbook/stack          local       -        -
```

## Deploy Stack

```bash
foo@bar:~$ monk run monk-vaultwarden/stack
? Select tag to run [local/growthbook/stack] on: mnk
✔ Starting the job: local/growthbook/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% growthbook/growthbook:latest mnk
✔ [================================================] 100% mongo:latest mnk
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Started local/growthbook/stack

🔩 templates/local/growthbook/stack
 └─🧊 Peer mnk
    ├─🔩 templates/local/growthbook/growthbook
    │  └─📦 aaf1b34cf8be374551539e3d6d6fbd19-ok-growthbook-monk-vaultwarden
    │     ├─🧩 growthbook/growthbook:latest
    │     ├─💾 /var/lib/monkd/volumes/growthbook -> /usr/local/src/app/packages/back-end/uploads
    │     ├─🔌 open <ip>:3100 (0.0.0.0:3100) -> 3100
    │     └─🔌 open <ip>:3000 (0.0.0.0:3000) -> 3000
    └─🔩 templates/local/growthbook/growthbook-db
       └─📦 0921ecdbc1abeef8f50ff0c1208b520d-ok-growthbook-db-monk-mongo-db
          └─🧩 mongo:latest

💡 You can inspect and manage your above stack with these commands:
 monk logs (-f) local/growthbook/stack - Inspect logs
 monk shell     local/growthbook/stack - Connect to the container's shell
 monk do        local/growthbook/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Check web gui

`http://<ip>:3000/`

## Variables

The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable          | Description                   | Defaults           |
|-------------------|-------------------------------|--------------------|
| jtw_secret        | Growthbook jwt secret         | monk               |
| growthbook_domain | Growthbook domain             | growthbook.monk.io |
| growthbook_http   | http protocol (http or https) | http               |
| growthbook_port1  | Growthbook port               | 3100               |
| growthbook_port2  | Growthbook port               | 3000               |
| db_password       | Database password             | monk               |

## Stop, remove and clean up workloads and templates

```bash
monk purge growthbook
```
