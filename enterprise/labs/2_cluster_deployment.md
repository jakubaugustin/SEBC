```
{
  "timestamp" : "2017-03-08T09:26:58.748Z",
  "clusters" : [ {
    "name" : "jakubaugustin",
    "version" : "CDH5",
    "services" : [ {
      "name" : "zookeeper",
      "type" : "ZOOKEEPER",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ ]
      },
      "roles" : [ {
        "name" : "zookeeper-SERVER-21ccb929c055ae1b858b01c68b43aa4e",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "b7480456-46ec-4bfb-ba06-ab1188e253f9"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4zg0rqybc631pis3qoj3i0laj"
          }, {
            "name" : "serverId",
            "value" : "1"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-3692d187eedc03bfb6dcaa580e1da923",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "4d0dee22-ac63-4cf8-b586-a21647b21f54"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "59ir9helf06ar3zo6yle3rgcz"
          }, {
            "name" : "serverId",
            "value" : "3"
          } ]
        }
      }, {
        "name" : "zookeeper-SERVER-87e88fe55c3bc625ac6fe281c0aafedd",
        "type" : "SERVER",
        "hostRef" : {
          "hostId" : "80bddef9-c95d-44dd-9db3-2895742a0e2a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7punc0oru2rhos0ydzxao4097"
          }, {
            "name" : "serverId",
            "value" : "2"
          } ]
        }
      } ],
      "displayName" : "ZooKeeper"
    }, {
      "name" : "hdfs",
      "type" : "HDFS",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "DATANODE",
          "items" : [ {
            "name" : "datanode_java_heapsize",
            "value" : "1073741824"
          }, {
            "name" : "dfs_data_dir_list",
            "value" : "/dfs/dn"
          }, {
            "name" : "dfs_datanode_bind_wildcard",
            "value" : "true"
          }, {
            "name" : "dfs_datanode_data_dir_perm",
            "value" : "755"
          }, {
            "name" : "dfs_datanode_du_reserved",
            "value" : "10736126771"
          }, {
            "name" : "dfs_datanode_max_locked_memory",
            "value" : "4294967296"
          }, {
            "name" : "dfs_datanode_use_datanode_hostname",
            "value" : "true"
          }, {
            "name" : "rm_cpu_shares",
            "value" : "200"
          }, {
            "name" : "rm_io_weight",
            "value" : "100"
          } ]
        }, {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "dfs_client_use_trash",
            "value" : "true"
          } ]
        }, {
          "roleType" : "JOURNALNODE",
          "items" : [ {
            "name" : "dfs_journalnode_edits_dir",
            "value" : "/dfs/jn"
          }, {
            "name" : "journalnode_bind_wildcard",
            "value" : "true"
          } ]
        }, {
          "roleType" : "NAMENODE",
          "items" : [ {
            "name" : "dfs_name_dir_list",
            "value" : "/dfs/nn"
          }, {
            "name" : "dfs_namenode_servicerpc_address",
            "value" : "8022"
          }, {
            "name" : "namenode_bind_wildcard",
            "value" : "true"
          } ]
        }, {
          "roleType" : "SECONDARYNAMENODE",
          "items" : [ {
            "name" : "fs_checkpoint_dir_list",
            "value" : "/data/hdd_0/dfs/snn"
          }, {
            "name" : "secondary_namenode_bind_wildcard",
            "value" : "true"
          } ]
        } ],
        "items" : [ {
          "name" : "dfs_client_use_datanode_hostname",
          "value" : "true"
        }, {
          "name" : "dfs_ha_fencing_cloudera_manager_secret_key",
          "value" : "aXtHiLgcnh17DBahY3xJv806dsVGv5"
        }, {
          "name" : "dfs_ha_fencing_methods",
          "value" : "shell(true)"
        }, {
          "name" : "fc_authorization_secret_key",
          "value" : "fXCxlNvgoy8mbERp5XqwVqGr91M7oJ"
        }, {
          "name" : "http_auth_signature_secret",
          "value" : "yKknQYn451fzK9ofYhPnHbZmKkIU6R"
        }, {
          "name" : "rm_dirty",
          "value" : "false"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "10"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hdfs-BALANCER-5100231a656dbaed4ff832444eeaef08",
        "type" : "BALANCER",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hdfs-DATANODE-21ccb929c055ae1b858b01c68b43aa4e",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "b7480456-46ec-4bfb-ba06-ab1188e253f9"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "dc6gaamynery3hk874s37xhg1"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-3692d187eedc03bfb6dcaa580e1da923",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "4d0dee22-ac63-4cf8-b586-a21647b21f54"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "7h4fq8yr7vurwnx2od23is7pi"
          } ]
        }
      }, {
        "name" : "hdfs-DATANODE-87e88fe55c3bc625ac6fe281c0aafedd",
        "type" : "DATANODE",
        "hostRef" : {
          "hostId" : "80bddef9-c95d-44dd-9db3-2895742a0e2a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "8w2p4upm2azid3ngtrlr4htnd"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-5100231a656dbaed4ff832444eeaef08",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4clh6ksk0gv8lh2y4d84lzay2"
          } ]
        }
      }, {
        "name" : "hdfs-FAILOVERCONTROLLER-75f78d21f31197354bfe8261918818d8",
        "type" : "FAILOVERCONTROLLER",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "auxr1ur8e01h3kfhta4c3mytd"
          } ]
        }
      }, {
        "name" : "hdfs-HTTPFS-5100231a656dbaed4ff832444eeaef08",
        "type" : "HTTPFS",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "579tnu32hcunzwwwwyrx8mei7"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-21ccb929c055ae1b858b01c68b43aa4e",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "b7480456-46ec-4bfb-ba06-ab1188e253f9"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9bmdz0lc16rer6yeavtdqgge3"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-3692d187eedc03bfb6dcaa580e1da923",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "4d0dee22-ac63-4cf8-b586-a21647b21f54"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "52furym4w82gyprtgc10b1axe"
          } ]
        }
      }, {
        "name" : "hdfs-JOURNALNODE-87e88fe55c3bc625ac6fe281c0aafedd",
        "type" : "JOURNALNODE",
        "hostRef" : {
          "hostId" : "80bddef9-c95d-44dd-9db3-2895742a0e2a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "4l6f3c8dktfl9ltg0odwg8ag9"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-5100231a656dbaed4ff832444eeaef08",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "jakub-ha"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "jakub-ha"
          }, {
            "name" : "namenode_id",
            "value" : "73"
          }, {
            "name" : "role_jceks_password",
            "value" : "87feilgenm0h23lynj7dvyocr"
          } ]
        }
      }, {
        "name" : "hdfs-NAMENODE-75f78d21f31197354bfe8261918818d8",
        "type" : "NAMENODE",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ {
            "name" : "autofailover_enabled",
            "value" : "true"
          }, {
            "name" : "dfs_federation_namenode_nameservice",
            "value" : "jakub-ha"
          }, {
            "name" : "dfs_namenode_quorum_journal_name",
            "value" : "jakub-ha"
          }, {
            "name" : "namenode_id",
            "value" : "24"
          }, {
            "name" : "role_jceks_password",
            "value" : "67rtmj9hkhtm2287ab9il35jf"
          } ]
        }
      } ],
      "displayName" : "HDFS"
    }, {
      "name" : "yarn",
      "type" : "YARN",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "GATEWAY",
          "items" : [ {
            "name" : "mapred_reduce_tasks",
            "value" : "6"
          }, {
            "name" : "mapred_submit_replication",
            "value" : "1"
          } ]
        }, {
          "roleType" : "NODEMANAGER",
          "items" : [ {
            "name" : "rm_cpu_shares",
            "value" : "1800"
          }, {
            "name" : "rm_io_weight",
            "value" : "900"
          }, {
            "name" : "yarn_nodemanager_heartbeat_interval_ms",
            "value" : "100"
          }, {
            "name" : "yarn_nodemanager_local_dirs",
            "value" : "/yarn/nm"
          }, {
            "name" : "yarn_nodemanager_log_dirs",
            "value" : "/yarn/container-logs"
          } ]
        }, {
          "roleType" : "RESOURCEMANAGER",
          "items" : [ {
            "name" : "resource_manager_java_heapsize",
            "value" : "52428800"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_mb",
            "value" : "2942"
          }, {
            "name" : "yarn_scheduler_maximum_allocation_vcores",
            "value" : "3"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "rm_dirty",
          "value" : "true"
        }, {
          "name" : "rm_last_allocation_percentage",
          "value" : "90"
        }, {
          "name" : "yarn_service_cgroups",
          "value" : "false"
        }, {
          "name" : "yarn_service_lce_always",
          "value" : "false"
        }, {
          "name" : "zk_authorization_secret_key",
          "value" : "loh2ZRwymy8FrLU6CKNr1TENG8oaLG"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "yarn-JOBHISTORY-5100231a656dbaed4ff832444eeaef08",
        "type" : "JOBHISTORY",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9sbrdvclf7qxm330t72j53x0l"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-21ccb929c055ae1b858b01c68b43aa4e",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "b7480456-46ec-4bfb-ba06-ab1188e253f9"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "3k4h8h7bvzupexfd1kdgh0f8i"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-3692d187eedc03bfb6dcaa580e1da923",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "4d0dee22-ac63-4cf8-b586-a21647b21f54"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "eh20p5thmpnmelwjne0mv4n2o"
          } ]
        }
      }, {
        "name" : "yarn-NODEMANAGER-87e88fe55c3bc625ac6fe281c0aafedd",
        "type" : "NODEMANAGER",
        "hostRef" : {
          "hostId" : "80bddef9-c95d-44dd-9db3-2895742a0e2a"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "5nsqp5rxii3civszsp5njjwos"
          } ]
        }
      }, {
        "name" : "yarn-RESOURCEMANAGER-75f78d21f31197354bfe8261918818d8",
        "type" : "RESOURCEMANAGER",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ {
            "name" : "rm_id",
            "value" : "38"
          }, {
            "name" : "role_jceks_password",
            "value" : "f3lereaj1lirxafn2pjbgf5or"
          } ]
        }
      } ],
      "displayName" : "YARN (MR2 Included)"
    }, {
      "name" : "hive",
      "type" : "HIVE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "HIVEMETASTORE",
          "items" : [ {
            "name" : "hive_metastore_java_heapsize",
            "value" : "2446327808"
          } ]
        }, {
          "roleType" : "HIVESERVER2",
          "items" : [ {
            "name" : "hiveserver2_java_heapsize",
            "value" : "2446327808"
          }, {
            "name" : "hiveserver2_spark_driver_memory",
            "value" : "966367641"
          }, {
            "name" : "hiveserver2_spark_executor_cores",
            "value" : "4"
          }, {
            "name" : "hiveserver2_spark_executor_memory",
            "value" : "3214881587"
          }, {
            "name" : "hiveserver2_spark_yarn_driver_memory_overhead",
            "value" : "102"
          }, {
            "name" : "hiveserver2_spark_yarn_executor_memory_overhead",
            "value" : "541"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_metastore_database_host",
          "value" : "node1.testcluster"
        }, {
          "name" : "hive_metastore_database_password",
          "value" : "password_for_hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hive-GATEWAY-21ccb929c055ae1b858b01c68b43aa4e",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "b7480456-46ec-4bfb-ba06-ab1188e253f9"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-3692d187eedc03bfb6dcaa580e1da923",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "4d0dee22-ac63-4cf8-b586-a21647b21f54"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-5100231a656dbaed4ff832444eeaef08",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-75f78d21f31197354bfe8261918818d8",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-GATEWAY-87e88fe55c3bc625ac6fe281c0aafedd",
        "type" : "GATEWAY",
        "hostRef" : {
          "hostId" : "80bddef9-c95d-44dd-9db3-2895742a0e2a"
        },
        "config" : {
          "items" : [ ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-5100231a656dbaed4ff832444eeaef08",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "99g31n8t0g7p7chdswnb8wu5f"
          } ]
        }
      }, {
        "name" : "hive-HIVEMETASTORE-75f78d21f31197354bfe8261918818d8",
        "type" : "HIVEMETASTORE",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2y9urzo6rwl9rrl1p3pequhqd"
          } ]
        }
      }, {
        "name" : "hive-HIVESERVER2-5100231a656dbaed4ff832444eeaef08",
        "type" : "HIVESERVER2",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "c4rgy2l1i8jmqvpp38hle40n5"
          } ]
        }
      } ],
      "displayName" : "Hive"
    }, {
      "name" : "sentry",
      "type" : "SENTRY",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "SENTRY_SERVER",
          "items" : [ {
            "name" : "sentry_server_java_heapsize",
            "value" : "268435456"
          } ]
        } ],
        "items" : [ {
          "name" : "hdfs_service",
          "value" : "hdfs"
        }, {
          "name" : "sentry_server_database_host",
          "value" : "node1.testcluster"
        }, {
          "name" : "sentry_server_database_password",
          "value" : "password_for_sentry"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "sentry-SENTRY_SERVER-75f78d21f31197354bfe8261918818d8",
        "type" : "SENTRY_SERVER",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "44lpd3w6x4fscwzftbqczlzn2"
          } ]
        }
      } ],
      "displayName" : "Sentry"
    }, {
      "name" : "oozie",
      "type" : "OOZIE",
      "config" : {
        "roleTypeConfigs" : [ {
          "roleType" : "OOZIE_SERVER",
          "items" : [ {
            "name" : "oozie_database_host",
            "value" : "node0.testcluster"
          }, {
            "name" : "oozie_database_password",
            "value" : "password_for_oozie"
          }, {
            "name" : "oozie_database_type",
            "value" : "mysql"
          }, {
            "name" : "oozie_database_user",
            "value" : "oozie"
          }, {
            "name" : "oozie_java_heapsize",
            "value" : "52428800"
          } ]
        } ],
        "items" : [ {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "mapreduce_yarn_service",
          "value" : "yarn"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "oozie-OOZIE_SERVER-5100231a656dbaed4ff832444eeaef08",
        "type" : "OOZIE_SERVER",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "9teerdahdo4fbwqv1ryz0fzdc"
          } ]
        }
      } ],
      "displayName" : "Oozie"
    }, {
      "name" : "hue",
      "type" : "HUE",
      "config" : {
        "roleTypeConfigs" : [ ],
        "items" : [ {
          "name" : "database_host",
          "value" : "node0.testcluster"
        }, {
          "name" : "database_password",
          "value" : "password_for_hue"
        }, {
          "name" : "database_type",
          "value" : "mysql"
        }, {
          "name" : "hive_service",
          "value" : "hive"
        }, {
          "name" : "hue_webhdfs",
          "value" : "hdfs-HTTPFS-5100231a656dbaed4ff832444eeaef08"
        }, {
          "name" : "oozie_service",
          "value" : "oozie"
        }, {
          "name" : "sentry_service",
          "value" : "sentry"
        }, {
          "name" : "zookeeper_service",
          "value" : "zookeeper"
        } ]
      },
      "roles" : [ {
        "name" : "hue-HUE_SERVER-5100231a656dbaed4ff832444eeaef08",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "i-0188fd0cdc639f1a3"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "2d4adi69y89vzja64ytc8hq1j"
          }, {
            "name" : "secret_key",
            "value" : "ECeLjW0aOgpAhbScekCS8JtQlEzecL"
          } ]
        }
      }, {
        "name" : "hue-HUE_SERVER-75f78d21f31197354bfe8261918818d8",
        "type" : "HUE_SERVER",
        "hostRef" : {
          "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
        },
        "config" : {
          "items" : [ {
            "name" : "role_jceks_password",
            "value" : "tjt5xywn1do23hk4zh9cx8kf"
          }, {
            "name" : "secret_key",
            "value" : "OIvLd4pn3T10zU8JBUw49fXSQslEKe"
          } ]
        }
      } ],
      "displayName" : "Hue"
    } ]
  } ],
  "hosts" : [ {
    "hostId" : "i-0188fd0cdc639f1a3",
    "ipAddress" : "172.31.1.215",
    "hostname" : "node0.testcluster",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5",
    "ipAddress" : "172.31.15.231",
    "hostname" : "node1.testcluster",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "b7480456-46ec-4bfb-ba06-ab1188e253f9",
    "ipAddress" : "172.31.9.230",
    "hostname" : "node2.testcluster",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "80bddef9-c95d-44dd-9db3-2895742a0e2a",
    "ipAddress" : "172.31.15.155",
    "hostname" : "node3.testcluster",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  }, {
    "hostId" : "4d0dee22-ac63-4cf8-b586-a21647b21f54",
    "ipAddress" : "172.31.2.140",
    "hostname" : "node4.testcluster",
    "rackId" : "/default",
    "config" : {
      "items" : [ ]
    }
  } ],
  "users" : [ {
    "name" : "__cloudera_internal_user__6f8450ab-9056-460f-b49a-0f7e79159f76",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "d98a58c3c1aefd81abdd6967e945549c146eab2e80c3e055ed09925c5129fdf7",
    "pwSalt" : 3194681428450615975,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-EVENTSERVER-75f78d21f31197354bfe8261918818d8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "28f9e7f01deb47d475fdd0e61a8a18cdf20c5b88010582e43effc3eb7e8f8ae8",
    "pwSalt" : -342620269386215411,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-HOSTMONITOR-75f78d21f31197354bfe8261918818d8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "8e64dfcedd840ac91f067bec078befc55f7c76d2fb8865059136c76bbfb59266",
    "pwSalt" : -6493239237080923144,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-REPORTSMANAGER-75f78d21f31197354bfe8261918818d8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "a9f4e4738735df5a283de9190178d416811f0d19675cf33e0dc27c117bbb71b6",
    "pwSalt" : -7408071194301043436,
    "pwLogin" : true
  }, {
    "name" : "__cloudera_internal_user__mgmt-SERVICEMONITOR-75f78d21f31197354bfe8261918818d8",
    "roles" : [ "ROLE_USER" ],
    "pwHash" : "72f12ea5bc2879c5705ebcb40c4ed32f39aa9533fd6f150a92e78c3efd8fc2ad",
    "pwSalt" : 1841756067369162441,
    "pwLogin" : true
  }, {
    "name" : "admin",
    "roles" : [ "ROLE_LIMITED" ],
    "pwHash" : "f13e74ef97dabf336b4784d24f570c3baae96b77d1f9d82fb83224832d089f5c",
    "pwSalt" : 1436513108442870590,
    "pwLogin" : true
  }, {
    "name" : "jakubaugustin",
    "roles" : [ "ROLE_ADMIN" ],
    "pwHash" : "07720ca8f2c842ed2e9b737575cbc6808ba806af64c292ef00d257c57cbbeaf4",
    "pwSalt" : 454723450891999740,
    "pwLogin" : true
  }, {
    "name" : "minotaur",
    "roles" : [ "ROLE_CONFIGURATOR" ],
    "pwHash" : "1190fb7220462898440ef6dd86806b817e53c3d896178a3b09e9f7835e413b91",
    "pwSalt" : 2460705352831682720,
    "pwLogin" : true
  } ],
  "versionInfo" : {
    "version" : "5.8.3",
    "buildUser" : "jenkins",
    "buildTimestamp" : "20161019-1013",
    "gitHash" : "518f0d6d44abc87bc392646e4369a20c8192b7cf",
    "snapshot" : false
  },
  "managementService" : {
    "name" : "mgmt",
    "type" : "MGMT",
    "config" : {
      "roleTypeConfigs" : [ {
        "roleType" : "HOSTMONITOR",
        "items" : [ {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1610612736"
        } ]
      }, {
        "roleType" : "REPORTSMANAGER",
        "items" : [ {
          "name" : "headlamp_database_host",
          "value" : "node1.testcluster"
        }, {
          "name" : "headlamp_database_name",
          "value" : "rman"
        }, {
          "name" : "headlamp_database_password",
          "value" : "password_for_rman"
        }, {
          "name" : "headlamp_database_user",
          "value" : "rman"
        } ]
      }, {
        "roleType" : "SERVICEMONITOR",
        "items" : [ {
          "name" : "firehose_non_java_memory_bytes",
          "value" : "1610612736"
        } ]
      } ],
      "items" : [ ]
    },
    "roles" : [ {
      "name" : "mgmt-ALERTPUBLISHER-75f78d21f31197354bfe8261918818d8",
      "type" : "ALERTPUBLISHER",
      "hostRef" : {
        "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "6vgljse3ujfl2wzzc9m3x428j"
        } ]
      }
    }, {
      "name" : "mgmt-EVENTSERVER-75f78d21f31197354bfe8261918818d8",
      "type" : "EVENTSERVER",
      "hostRef" : {
        "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "7zwx7rmn18mclv0kj5ztzhuw7"
        } ]
      }
    }, {
      "name" : "mgmt-HOSTMONITOR-75f78d21f31197354bfe8261918818d8",
      "type" : "HOSTMONITOR",
      "hostRef" : {
        "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "76qq0fss3fysnfkuuho93lj5w"
        } ]
      }
    }, {
      "name" : "mgmt-REPORTSMANAGER-75f78d21f31197354bfe8261918818d8",
      "type" : "REPORTSMANAGER",
      "hostRef" : {
        "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "7opeaqw5612wbyksdeegj7iwt"
        } ]
      }
    }, {
      "name" : "mgmt-SERVICEMONITOR-75f78d21f31197354bfe8261918818d8",
      "type" : "SERVICEMONITOR",
      "hostRef" : {
        "hostId" : "c630e19b-ea05-4aa2-beb3-bcdc86fe91e5"
      },
      "config" : {
        "items" : [ {
          "name" : "role_jceks_password",
          "value" : "6ij5q26z7k658xdya3t0x3wyi"
        } ]
      }
    } ],
    "displayName" : "Cloudera Management Service"
  },
  "managerSettings" : {
    "items" : [ {
      "name" : "CLUSTER_STATS_START",
      "value" : "10/24/2012 20:50"
    }, {
      "name" : "PUBLIC_CLOUD_STATUS",
      "value" : "ON_PUBLIC_CLOUD"
    }, {
      "name" : "REMOTE_PARCEL_REPO_URLS",
      "value" : "https://archive.cloudera.com/cdh5/parcels/{latest_supported}/,http://node0.testcluster/parcels/5.8.3/"
    } ]
  }
}
```