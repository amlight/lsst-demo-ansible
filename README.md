
## LSST 2017 EoY demo

You can find some Ansible playbooks for generating traffic with nuttcp and iperf3 for the LSST demo in 2017. In order to generate bidirectional traffic, you should have access to both servers.

## nuttcp examples

The main playbook is `nuttcp.yml`. Host specific configuration for each flow is under host_vars, for example destination IP address, control and data plane port. In the same way, global variables are set in the playbook itself.

### To kill all nuttcp process, servers and data tranfers

```
ansible-playbook killall_nuttcp.yml --user=LOCALUSER --forks=6
```

### Starting nuttcp data transfers on all DTNs bidirectionally

```
ansible-playbook nuttcp.yml --user=LOCALUSER --forks=6
```

### Starting nuttcp data transfers limiting one DTN unidirectionally

```
ansible-playbook nuttcp.yml --user=LOCALUSER --limit=ps-bw.l3-santiago.ampath.net --forks=6
```

### Overriding flow_bw to 2G per flow

```
ansible-playbook nuttcp.yml --user=LOCALUSER -e=flow_bw=2G -vv --forks=6
```

## iperf3 examples

### Unidirectional traffic:

```
ansible-playbook iperf3.yml --user=LOCALUSER --limit=ps-bw.l3-santiago.ampath.net -vv --forks=6
```

### Bidirectional traffic:

```
ansible-playbook iperf3.yml --user=LOCALUSER -vv --forks=6
```


