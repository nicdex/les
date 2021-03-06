# LES

## _"Let's Event Source Together"_

* Validates the design of an event-based system specified in Event Markdown or Event Markup Language.
* Generates an API from Event Markdown or Event Markup
* [LESTER Stack FAQ](https://github.com/Adaptech/letseventsource)


![LESTER Pipeline](https://github.com/Adaptech/letseventsource/blob/master/LESTER-stack-diagram.png)

## Getting Started

### Prerequisites

* [NodeJS 8.11.1 LTS](https://nodejs.org/en/) or better
* [docker-compose](https://docs.docker.com/compose/install/)

### Installation

[Instructions for Linux, Windows Mac & Docker](INSTALL.md)

### Hello World

**Step 1:**

```bash
cat <<EOT >> Eventstorming.emd
# Hello World
Say Hello World->
HelloWorld Said
EOT
```

**Step 2:**

```bash
les convert && les-node -b && cd api && npm install && docker-compose up -d
```

Or using Docker:
```bash
docker run -v $(pwd):/les les convert && docker run -v $(pwd):/les les-node -b && cd api && npm install && docker-compose up -d
```

(If you doing this in Linux and encounter "permission denied" errors, your USER or GROUP ID need to be specified.
 Say your USER ID is 1003, then add `--user 1003` after each `docker run` in the above command.)

**Step 3:**

There is no step 3.

* Swagger/OpenAPI docs for the new API: http://localhost:3001/api-docs
* Source Code: ./api
* API URI: http://localhost:3001/api/v1
* Eventstore DB: http://localhost:2113 (username 'admin', password 'changeit')

## What next ...

* Learn Event Storming: http://eventstorming.com

* Learn Event Markdown (EMD): https://webeventstorming.com

* EMD Examples: https://github.com/Adaptech/les/src/master/samples**

* EMD Cheat Sheet: https://github.com/Adaptech/letseventsource/raw/master/EMD-Cheatsheet-0.10.0-alpha-alpha.pdf

## IDE Integrations & Tools

* Event Markdown [vscode extension](https://github.com/markgukov/vscode-event-markdown)


## Known UX Impacting Issues

The issues below have been known to mystify EMD users:

#### "DromedaryCase": myaggregateId GOOD, myAggregateId BAD

https://github.com/Adaptech/les/issues/9

#### Sporadic Race condition when doing ```cd api && npm install && docker-compose up -d```

API doesn't start because Eventstore isn't up yet. (Workaround: ```docker-compose restart api```)

https://github.com/Adaptech/les/issues/11

#### Need to have at least one read model parameter which is not an aggregate ID

https://github.com/Adaptech/les/issues/10
