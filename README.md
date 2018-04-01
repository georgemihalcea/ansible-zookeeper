# ansible-zookeeper

Ansible playboot that installs zookeeper (single instance or cluster) from https://zookeeper.apache.org/.
It works with Debian and Ubuntu.

It downloads the install package from a mirror, checks the sha256 sum, extracts the package to /opt (or whatever path is set in the "zookeeper_base" variable), creates the config file, data directory, myid file, log directory, user, group, systemd unit file, installs the required java packages, enables and starts the zookeeper service.

The setting valid for all servers are in group_vars/all file, and the individual settings for each server are in host_vars/<hostname> files.
The only setting that is unique is the server id in the cluster, that will be set in the <zookeeper_data_dir>/myid file.

Sample settings for group_vars/all:

    ---
    # general settings
    zookeeper_service: zookeeper
    java_package: openjdk-8-jdk
    zookeeper_package_url: http://apache.mirror.digionline.de/zookeeper/zookeeper-3.4.11/zookeeper-3.4.11.tar.gz
    zookeeper_package: /var/tmp/zookeeper-3.4.11.tar.gz
    zookeeper_base: /opt
    zookeeper_folder: /opt/zookeeper-3.4.11
    zookeeper_path: /opt/zookeeper
    zookeeper_user: zookeeper
    zookeeper_group: zookeeper
    zookeeper_user_uid: 610
    zookeeper_user_gid: 610
    
    # config file settings
    zookeeper_tick_time: 2000
    zookeeper_init_limit: 10
    zookeeper_sync_limit: 5
    zookeeper_data_dir: /var/lib/zookeeper
    zookeeper_client_port: 2181
    zookeeper_servers:
      1:
        hostname: zookeeper01.example.net
        leader_port: 2888
        follower_port: 3888
      2:
        hostname: zookeeper02.example.net
        leader_port: 2888
        follower_port: 3888
      3:
        hostname: zookeeper03.example.net
        leader_port: 2888
        follower_port: 3888
      4:
        hostname: zookeeper04.example.net
        leader_port: 2888
        follower_port: 3888
      5:
        hostname: zookeeper05.example.net
        leader_port: 2888
        follower_port: 3888

