## free Command

How much free RAM memory do I have available on my Linux system? Is there enough free memory to install and run new applications?
In Linux systems, you can use the free command to get a detailed report on the system’s memory usage.
The free command provides information about the total amount of the physical and swap memory, as well as the free and used memory.

```bash
# default (without options), it will display memory and swap in KBs
free
```
Following is the sample output
```bash
              total        used        free      shared  buff/cache   available
Mem:       16160564    10173712      294888     1212984     5691964     4436908
Swap:        999420      221696      777724
```

Headers make sense what is represented in output but let me define two confusing, or not-familiar-to-everybody thing, headers;

**shared** This column can be ignored as it has no meaning. It is here only for backward compatibility.

**buff/cache** The combined memory used by the kernel buffers and page cache and slabs. This memory can be reclaimed at any time if needed by the applications. If you want buffers and cache to be displayed in two separate columns, use the -w option.

### Available Options
-b,-k,-m,-g show output in bytes, KB, MB, or GB
-l show detailed low and high memory statistics
-o use an old format (no -/+buffers/cache line)
-t display total for RAM + swap
-s update every [delay] seconds
-c update [count] times
```
