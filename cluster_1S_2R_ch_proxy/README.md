# Cluster Clickhouse dengan 1 Shard dan 2 Replikasi/ClickHouse instances


2 Replikasi yang memanfaatkan 3 ClickHouse Keepers untuk Manajemen Klaster dan CH Proxy sebagai load balancer


1. Copy dan rename .env.example menjadi .env di root folder
2. ada 4 variable di dlam .env silahkan di sesuaikan
    USERNAME_PROXY=username-proxy
    PASSWORD_PROXY=password-proxy
    USERNAME_NODES=username-nodes
    PASSWORD_NODES=password-nodes
3. buka file users.xml di dalam folder clickhouse-01/etc/clickhouse-server/user.d/user.xml
   edit bagian tag users sesuikan dengan
   - ENV USERNAME_NODES
   - PASSWORD_NODES
        Note : untuk  password_sha256_hex itu sha256_hex dari env  PASSWORD_NODES.
        kamu bisa generate pakai link ini : https://passwordsgenerator.net/sha256-hash-generator/
    <username-nodes>
        <access_management>1</access_management>
        <profile>default</profile>
        <networks>
            <ip>::/0</ip>
        </networks>
        <quota>default</quota>
        <!-- sha256_hex from string "password" -->
        <password_sha256_hex>58C74D9729258537D514F717F00E49727F7F2B1AD5FC3AC59F78047DA12D4D73</password_sha256_hex> 
        <access_management>1</access_management>
        <named_collection_control>1</named_collection_control>
        <show_named_collections>1</show_named_collections>
        <show_named_collections_secrets>1</show_named_collections_secrets>
    </username-nodes>

    Lakukan hal yg salam untuk file users.xml di dalam folder clickhouse-02/etc/clickhouse-server/user.d/user.xml