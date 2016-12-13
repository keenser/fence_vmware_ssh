# fence_vmware_ssh
redhat cluster fence agent for vmware esxi over SSH using "vim-cmd"  for power management
fence_vmware_soap replacement. No vcenter required.
# Usage
You need installed fence-agents rpm on cluster VMs
copy fence_vmware_ssh to /usr/sbin on cluster VMs
enable ssh on esxi host
test fencing on VM with name 'test':
$ fence_vmware_ssh -a 192.168.1.10 -l root -p pass -o list
$ fence_vmware_ssh -a 192.168.1.10 -l root -p pass -o status -n test
$ fence_vmware_ssh -a 192.168.1.10 -l root -p pass -o reboot -n test
$ fence_vmware_ssh -a 192.168.1.10 -l root -p pass -o reboot -n test -m cycle
$ fence_vmware_ssh -a 192.168.1.10 -l root -p pass -o on -n test
$ fence_vmware_ssh -a 192.168.1.10 -l root -p pass -o off -n test

modify cluster.conf like:
      &lt;clusternodes&gt;
              &lt;clusternode name="node1" nodeid="1" votes="1"&gt;
                      &lt;fence&gt;
                              &lt;method name="1"&gt;
                                      &lt;device name="vmware1"/&gt;
                              &lt;/method&gt;
                      &lt;/fence&gt;
              &lt;/clusternode&gt;
              &lt;clusternode name="node2" nodeid="2" votes="1"&gt;
                      &lt;fence&gt;
                              &lt;method name="1"&gt;
                                      &lt;device name="vmware2"/&gt;
                              &lt;/method&gt;
                      &lt;/fence&gt;
              &lt;/clusternode&gt;
      &lt;/clusternodes&gt;
      &lt;fencedevices&gt;
              &lt;fencedevice agent="fence_vmware_ssh" ipaddr="esxi host IP" login="root" passwd="pass" name="vmware1" port="VMname1"/&gt;
              &lt;fencedevice agent="fence_vmware_ssh" ipaddr="esxi host IP" login="root" passwd="pass" name="vmware2" port="VMname2"/&gt;
      &lt;/fencedevices&gt;

