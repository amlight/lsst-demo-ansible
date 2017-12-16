
## LSST 2017 EoY demo

You can find some Ansible playbooks for generating traffic with nuttcp for the LSST demo in 2017.

## nuttcp Examples

The main playbook is `nuttcp.yml`. Host specific configuration for each flow is under host_vars, for example destination IP address, control and data plane port. In the same way, global variables are set in the playbook itself.

### To kill all nuttcp process, servers and data tranfers

```
ansible-playbook killall.yml --user=LOCALUSER --forks=6
```

### Starting nuttcp data transfers on all hosts bidirectional

```
ansible-playbook nuttcp.yml --user=LOCALUSER --forks=6
```

### Starting nuttcp data transfers limiting one server, unidirectional

```
ansible-playbook nuttcp.yml --user=LOCALUSER --limit=ps-bw.l3-santiago.ampath.net --forks=6
```

### Overriding flow_bw to 2G per flow

```
ansible-playbook nuttcp.yml --user=LOCALUSER -e=flow_bw=2G -vv --forks=4
```
