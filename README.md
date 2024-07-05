# Domains subgraph

## Current supported domains

| Subgraph Name | Network | TLD      | Note |
|---------------|---------|----------|------|
| zns-subgraph  | Arthera | .arthera |      |

## Deploy subgraph to graph-node

> It's posibble to deploy subgraph to graph-node

1. Initially:

    ```bash
    yarn install
    yarn codegen
    yarn build
    ```

2. Run your own `graph-node` using docker

3. Create subgraph on graph-node

    ```bash
    yarn run create
    ```

4. Deploy subgraph to local graph-node

    ```bash
    yarn run deploy
    ```

5. Check errors and result:

    + Connect to subgraph playground and check current state of deployed subgraph by querying the metadata

    + Connect to subgraph database and check current state of deployed subgraph:

        ```postgres
        select deployment, failed, health, synced, latest_ethereum_block_number, fatal_error from subgraphs.subgraph_deployment;
        
        select * from subgraphs.subgraph_error;
        
        select name, resolved_address, expiry_date 
        from sgd1.domain 
        where label_name is not null and block_range @> 2147483647 
        order by created_at 
        limit 100;
        ```
