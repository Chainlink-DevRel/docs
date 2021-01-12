# Quick start
Learn the basics by setting up and interacting with the Ceramic CLI.

!!! note ""
    This tutorial serves as a simple introduction to Ceramic concepts and
    intentionally simplifies things. See [installation](./installation.md) to
    fully configure your client.

## Prerequisites

This quick start guide will use a terminal, [Node.js](https://nodejs.org/en/), and [npm](https://www.npmjs.com/get-npm). Make sure
to have these installed on your machine.

## Install the CLI

Install the Ceramic CLI using your terminal.

```bash
npm install -g @ceramicnetwork/cli
```

## Start the daemon

Start a Ceramic daemon on your local machine and automatically connect to it on
port 7007, `http://localhost:7007`.

```bash
ceramic daemon
```

??? note "Node configurations"
    There are multiple options you can configure when you start the ceramic daemon.
    
    - **Network**: By default the CLI starts a Ceramic node on the `clay` testnet. If you
    would like to use a different Ceramic network, you can specify this with the
    `--network` option.
    - **Additional configurations**: Use the `ceramic daemon -h` command to see additional options.


## Authentication
By default, the Ceramic CLI is authenticated with a
[Key DID](https://github.com/ceramicnetwork/key-did-provider-ed25519){:target="_blank"}. The seed
for this DID is stored in `~/.ceramic/config.json`. If this file is not present
on startup a new DID will be randomly generated. It's currently not possible to
use the Ceramic CLI with other DID methods.


## Create a document
Use the `create` command to create a new document. In the example below
we create a document using the *tile* doctype.

=== "Request"

    ```bash
    $ ceramic create tile --content '{ "Foo": "Bar" }'
    ```

=== "Response"

    ```bash
    DocID(kjzl6cwe1jw14a80400xpbj97sutzdssg9rklbyykj0zdxzbpmww4x9e9w4vcyr)
    {
        "Foo": "Bar"
    }
    ```

    The first line of the output is the *DocID*, which is the persistent identifier of our newly created document. This DocID will be different for you, since you created it with your DID. Below the DocID is the current content of the document.

??? note "More options"
    You can specify the *controller* and *schema* of the document by using the
    `--controllers` and `--schema` options respectively. Run `ceramic create -h`
    to see all available options.

## Query a document
Use the `show` command to query the current state of a document. You will need to provide its *DocID*.

=== "Request"

    ```bash
    $ ceramic show kjzl6cwe1jw14a80400xpbj97sutzdssg9rklbyykj0zdxzbpmww4x9e9w4vcyr
    ```
    
    You should use your DocID instead of the DocID included here.

=== "Response"

    ```bash
    {
        "Foo": "Bar"
    }
    ```


Use the `state` command to query the entire state of a document.

=== "Request"

    ```bash
    $ ceramic state kjzl6cwe1jw14a80400xpbj97sutzdssg9rklbyykj0zdxzbpmww4x9e9w4vcyr
    ```
    
    You should use your DocID instead of the DocID included here.

=== "Response"

    {
      "doctype": "tile",
      "content": {
        "Foo": "Bar"
      },
      "metadata": {
        "schema": null,
        "controllers": [
          "did:key:z6MkfZ6S4NVVTEuts8o5xFzRMR8eC6Y1bngoBQNnXiCvhH8H"
        ]
      },
      "signature": 2,
      "anchorStatus": "PENDING",
      "log": [
        {
          "cid": "bagcqceray2cbrwx45oa5nesee4s4cggkodmsttzuqfzh32yat3o26iw5m5rq",
          "type": 0
        }
      ],
      "anchorScheduledFor": "1/11/2021, 11:45:00 AM"
    }
    ```
    
    In your response you should see your DID as the controller, instead of the DID we show here.

!!! note ""
    Here we can see various information about the document such as *content*,
    *controllers*, and *schema*. We can also see the current *anchorStatus* of our
    document. Above we see that our document has been scheduled to be anchored at
    11:45 on the 11th of January 2021. Once this anchor is finalized, the state of the document will be updated
    with a new entry in the log and *anchorStatus* will be set to `ANCHORED`.


## Update a document
You can update documents which you are the controller of. In order to do this
you use the `change` command.

```jsx

```

??? note "More options"
    Currently you can change *content*, *controllers*, and *schema* using the
    cli. Run `ceramic change -h` for more information.


## Create a schema
In Ceramic you can enforce that documents follow a specific schema. The schemas
themselves are Ceramic documents where the content is a
[json-schema](https://json-schema.org/){:target="_blank"}. For example we can create a schema that
requires a document to have a *title* and a *message*.

```jsx

```

## Create a document that uses a schema
To create a document which uses the schema we just created above we simply use
the `--schema` option to pass the DocID at a specific commit of a schema. In
order to get the specific commitId we use the `ceramic commits` command.

```jsx

```

## Query the document you created
Now if we look at the state of the document we just created we can see that the
schema is set to the correct DocID.

```jsx

```

# That's it!
Congratulations on completing this tutorial! You're well on your way to becoming a Ceramic developer. Now let's [install Ceramic in your project →](./installation.md).
</br>
</br>
</br>
