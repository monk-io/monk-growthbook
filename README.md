# Gost & Monk
This repository contains Monk.io template to deploy gost either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Clone Repository
```bash
git clone https://github.com/Burakhan/monk-gost
```

## Load Template
```bash
cd monk-gost
monk load MANIFEST
```


#### Let's take a look at the themes I have installed.
```bash
foo@bar:~$ monk list monk-gost
✔ Got the list
Type      Template         Repository  Version  Tags
runnable  monk-gost/gost   local       -        -
group     monk-gost/stack  local       -        -
```

## Deploy Stack
```bash
foo@bar:~$ monk run monk-gost/stack
? Select tag to run [local/monk-gost/stack] on: mnk
✔ Starting the job: local/monk-gost/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% ginuerzh/gost:latest mnk
✔ Checking/pulling images DONE
✔ Started local/monk-gost/stack

🔩 templates/local/monk-gost/stack
 └─🧊 Peer mnk
    └─🔩 templates/local/monk-gost/gost
       └─📦 570b584e7ce6813b7b8dfe68027d1bd0-local-monk-gost-gost-monk-gost
          ├─🧩 ginuerzh/gost:latest
          └─🔌 open 13.50.100.228:8080 (0.0.0.0:8080) -> 80

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) local/monk-gost/stack - Inspect logs
	monk shell     local/monk-gost/stack - Connect to the container's shell
	monk do        local/monk-gost/stack/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Variables
The variables are in `stack.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                               	|
|------------------------------	|-------------------------------------------	|
| expose_port                    | MSSQL database port, Default: 1433 	               |


## Stop, remove and clean up workloads and templates

```bash
monk purge -x -a
```

