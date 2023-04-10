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

```bash
foo@bar:~$ monk list growthbook
✔ Got the list
Type      Template                  Repository  Version  Tags
runnable  growthbook/growthbook     local       -        A/B testing, Conversion optimization, Experimentation, Growth hacking, Analytics, User engagement, Product optimization, Data-driven decision making, Personalization, Customer insights, Marketing optimization, Funnel optimization, Performance tracking, Website optimization, Conversion rate optimization
runnable  growthbook/growthbook-db  local       -        NoSQL, Document database, Database management, JSON, Scalability, High availability, Performance optimization, Indexing, Sharding, Aggregation, Replication, Data modeling, Cloud database, Big data
group     growthbook/stack          local       -        A/B testing, Conversion optimization, Experimentation, Growth hacking, Analytics, User engagement, Product optimization, Data-driven decision making, Personalization, Customer insights, Marketing optimization, Funnel optimization, Performance tracking, Website optimization, Conversion rate optimization
```

## Deploy Stack

```bash
foo@bar:~$ monk run monk-vaultwarden/stack
? Select which 'growthbook/stack' to run local/growthbook/stack
✔ Starting the run job: local/growthbook/stack... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% mongo:4.4 local
✔ [================================================] 100% growthbook/growthbook:latest local
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ New container local-9211f08d68e7ede3744bb8599c-ok-growthbook-db-monk-mongo-db created DONE
✔ New container local-c5654f9095967143fe7abdbaed-owthbook-growthbook-growthbook created DONE
✔ Started local/growthbook/stack
🔩 templates/local/growthbook/stack
 └─🧊 Peer local
    ├─🔩 templates/local/growthbook/growthbook
    │  └─📦 local-c5654f9095967143fe7abdbaed-owthbook-growthbook-growthbook running
    │     ├─🧩 growthbook/growthbook:latest
    │     └─💾 /var/lib/monkd/volumes/growthbook/data -> /usr/local/src/app/packages/back-end/uploads
    └─🔩 templates/local/growthbook/growthbook-db
       └─📦 local-9211f08d68e7ede3744bb8599c-ok-growthbook-db-monk-mongo-db running
          ├─🧩 mongo:4.4
          └─💾 /var/lib/monkd/volumes/growthbook/mongo -> /data/db

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
| ----------------- | ----------------------------- | ------------------ |
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
