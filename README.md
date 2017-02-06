# cuda-collectd

`cuda-collectd` is a `collectd-python` plugin for pushing statistics from 
the `nvidia-smi` utility to collectd. 

This project is forked from `sajkec/cuda-collectd`and changed to comply
with my configuration and needs.

## installation

Requires `collectd-python` package. On Centos 7,

    $ yum install collectd-python

While this is somewhat environment specific, based on the configuration 
in `10-cuda.conf`, the module files should be located inside `/usr/lib/collectd`,

    $ cp cuda_collectd.py /usr/lib/collectd/

The configuration file (10-cuda.conf) should be either placed in a path that is
included within collectd.conf, for e.g. if it there is a line in collectd.conf
such as - 
``` Include "/etc/collectd/managed_config/*.conf" ``` 
then 10-cuda.conf should be placed in the managed_config folder.
    
Use puppet to create module files or manually create one,    

    $ vim 10-cuda.conf
    
    LoadPlugin python		
		
    <Plugin python>		
        ModulePath "/usr/lib/collectd.d"
        Interactive False		
        Import "cuda_collectd"		
    </Plugin>
