# Installation
Install a client to interact with the Ceramic network.

## Clients
Ceramic is available in a variety of clients suited for different use cases. For optimal performance, it is recommended that you use the HTTP Client during runtime.

Client | Description | Usage | Details |
| ------ | ----- | ---- | --- |
| HTTP | An API for interacting with a remote Ceramic daemon over HTTP | Runtime | [Learn]() |
| Core | An API for interacting with a Ceramic node in a local JavaScript environment, such as directly in-browser | Runtime | [Learn]() |
| CLI | A command line interface for interacting with a Ceramic node | Development | [Learn]() |

## Installation
Open your terminal and install a client using npm.

=== "HTTP"

    ``` bash
    $ npm install @ceramicnetwork/http-client
    ```

=== "Core"

    ``` bash
    $ npm install @ceramicnetwork/core
    ```

=== "CLI"

    ``` bash
    $ npm install -g @ceramicnetwork/cli
    ```

    The CLI requires the use of Node.js. Make sure to have an up-to-date version installed on your machine.

## Setup
Setup your client within your project.

=== "HTTP"

    #### Import the HTTP client

    ``` javascript
    import CeramicClient from '@ceramicnetwork/http-client'
    ```

    #### Connect to a node

    ``` javascript
    const API_URL = "http://yourceramicnode.com"
    ```
    
    !!! note "Node options"
        When using the HTTP API, you need to connect to a remote Ceramic node by passing its URL. Here are your options for nodes that run on the Clay testnet. Choose the option that best suits your use case:
        
        - Community gateway `https://ceramic-clay-gateway.3boxlabs.com`: Provides read-only access to the Clay testnet.
        - Comunity dev node `https://ceramic-clay-dev.3boxlabs.com`: Provides write and read access to the Clay testnet. This node is periodically wiped and does not guarantee document persistence.
        - Run your own node `https://yourEndpoint.com`: Provides write and read access to the Clay testnet. Running your own node allows you to persist documents and have full control.
        - LocalHost `https://localhost:7007`: Provides write and read access to the Clay testnet. Users need to first have a Cermic daemon running locally using the CLI.

    #### Create an instance

    ``` javascript
    const ceramic = new CeramicClient(API_URL)
    ```

=== "Core"

    #### Import the Core client

    ``` javascript
    import Ceramic from '@ceramicnetwork/core'
    ```

    #### Import IPFS with dag-jose
    Ceramic utilizes the [dag-jose](https://github.com/ipld/specs/blob/master/block-layer/codecs/dag-jose.md){:target="_blank"}
    IPLD codec to store signed and encrypted data in IPFS. In order to create an
    instance of Ceramic core, you first need to create an instance of *js-ipfs*
    with *dag-jose* enabled.

    ``` javascript
    import IPFS from 'ipfs'
    import dagJose from 'dag-jose'
    import basicsImport from 'multiformats/cjs/src/basics-import.js'
    import legacy from 'multiformats/cjs/src/legacy.js'

    basicsImport.multicodec.add(dagJose)
    const format = legacy(basicsImport, dagJose.name)
    ```

    #### Create an IPFS instance

    ``` javascript
    const ipfs = Ipfs.create({
        ipld: { formats: [format] },
    })
    ```

    #### Create a Ceramic instance
    Create an instance of Ceramic by passing ipfs and an optional configuration
    object.

    ``` javascript
    const ceramic = await Ceramic.create(ipfs, config)
    ```

=== "CLI"

    #### Start the Ceramic daemon

    ```bash
    ceramic daemon
    ```

    #### Connect to a Ceramic node
    TODO: FIX THIS

    ```bash
    --API_URL(https://yourceramicnode.com)
    ```

    !!! note "Node options"
        When using the CLI, you need to connect to a remote Ceramic node by passing its URL. Here are your options for nodes that run on the Clay testnet. Choose the option that best suits your use case:
        
        - LocalHost `https://localhost:7007`: Enabled by default. Provides write and read access to the Clay testnet.
        - Community gateway `https://ceramic-clay-gateway.3boxlabs.com`: Provides read-only access to the Clay testnet.
        - Comunity dev node `https://ceramic-clay-dev.3boxlabs.com`: Provides write and read access to the Clay testnet. This node is periodically wiped and does not guarantee document persistence.
        - Run your own node `https://yourEndpoint.com`: Provides write and read access to the Clay testnet. Running your own node allows you to persist documents and have full control.

## Examples

TODO - what do we want to do with these examples?

Your project should look something like this. You may have slight modifications
depending on your configuration.

=== "HTTP"

    ``` javascript
    import CeramicClient from '@ceramicnetwork/http-client'
    ```

=== "Core"

    ``` javascript
    import Ceramic from '@ceramicnetwork/core'
    ```

=== "CLI"

    ```bash
    ceramic daemon
    ```

</br>
</br>
