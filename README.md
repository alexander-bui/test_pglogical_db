# test_pglogical_db

### Notes
Run `docker network create pg_logic` to set up the network

Local:
Need to be on the same docker network (as written in compose) and port 5432

For External, use external ip and external port

----
## Commands

On Host
-----
CREATE EXTENSION pglogical;

select pglogical.create_node(node_name := 'provider1', dsn := 'host=pg_master port=5431 dbname=sample_db user=postgres password=testing101');

SELECT pglogical.replication_set_add_all_tables('default', ARRAY['public']);

grant usage on schema pglogical to postgres;

select pglogical.drop_node('provider1');

On Slave
----
CREATE EXTENSION pglogical;

SELECT pglogical.create_node(
    node_name := 'subscriber1',
    dsn := 'host=pg_slave port=5432 dbname=sample_db user=postgres password=testing111'
);

### LOCAL
SELECT pglogical.create_subscription(
    subscription_name := 'subscription1',
    provider_dsn := 'host=pg_master port=5432 dbname=sample_db user=postgres password=testing101'
);

### EXTERNAL
SELECT pglogical.create_subscription(
    subscription_name := 'subscription1',
    provider_dsn := 'host=external_ip port=5431 dbname=sample_db user=postgres password=testing101'
);

select pglogical.drop_node('subscriber1');

select pglogical.drop_subscription('subscription1');

select 'subscription1', status FROM pglogical.show_subscription_status();

SELECT pglogical.wait_for_subscription_sync_complete('subscription1');

select * FROM pglogical.show_subscription_status();