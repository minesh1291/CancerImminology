# Script to submit job on SGE (Sun Grid Engine) Cluster
not a best practice but what we are supposed to use


## Edit the following script so it reflects one run of your parallelized software:

* wrapper.csh: make sure to make it executable

```bash

#!/bin/tcsh

set ITER_NUM=$1;

set COMMAND_1="./Learner.v1.py";

/storage/users/erubin/python/bin/python3.6 $COMMAND_1 $ITER_NUM

```


## Edit the following script so it reflects the number of runs you want to submit. Currently, the cluster will not allow more than 400:

* runner.csh: edit the first (j = 1) and last (<=1000) values to set the from-to iterations. We use 1..1000


```bash

set j = 1

while ( $j <= 1000 )

   echo "qsub -cwd -q bioinfo.q -j Y wrapper.csh $j"

   @ j++

end

```

## Run the following from the command line

```bash
tcsh runner.csh > do
bash do
```
