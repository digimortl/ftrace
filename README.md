## Simple ftrace script

### Usage
```bash
# ./ftrace                                         
Usage: ftrace start [-g|--graph] [PROGRAM|PID]
Usage: ftrace stop
```

### Starting ftrace for a program
```bash
# ./ftrace start --graph cat /515f5cfd/a.txt
function_graph tracer enabled
tracee: cat /515f5cfd/a.txt
cat /515f5cfd/a.txt: Input/output error
```

### Starting ftrace for a running process (by PID)
```bash
# ./ftrace -g start 1
function_graph tracer enabled
tracee: PID 1
```

### Stopping ftrace
```bash
# ./ftrace stop
Tracer disabled, check trace.txt file.
```

### Checking collected traces
```bash
# cat trace.txt
...
 7)               |  __x64_sys_openat() {
 7)               |    do_sys_openat2() {
 7)               |      getname() {
 7)   0.161 us    |        __audit_reusename();
 7)               |        getname_flags.part.0() {
 7)               |          kmem_cache_alloc() {
...
 7)   0.165 us    |                      __cond_resched();
 7)   0.269 us    |                      __ext4_error_inode [ext4]();
 7)   0.174 us    |                      __brelse();
 7) + 51.008 us   |                    }
...
 7)               |      put_unused_fd() {
 7)   0.180 us    |        _raw_spin_lock();
 7)   0.167 us    |        _raw_spin_unlock();
 7)   0.834 us    |      }
 7)   0.160 us    |      putname();
 7) ! 136.884 us  |    }
 7) ! 137.267 us  |  }
...
```
