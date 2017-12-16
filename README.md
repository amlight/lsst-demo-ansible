
## LSST 2017 EoY demo

You can find some Ansible playbooks for generating traffic with nuttcp and iperf3 for the LSST demo in 2017. In order to generate bidirectional traffic:

- for nuttcp, you should have ssh access on all DTNs/servers.
- for iperf3, as long as you can manage one DTN/server pair is enough since this playbook leverages the reverse option.

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

Since this playbooks leverages the reverse option to start the traffic in the opposite direction, you should limit to a single DTN:

```
ansible-playbook iperf3.yml --user=LOCALUSER --limit=ps-bw.l3-santiago.ampath.net -vv --forks=6
```

