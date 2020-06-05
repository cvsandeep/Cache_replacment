# Cache_replacment
RRIP and ARC cache replacement

Usage: 
The cache config parameter <config> has the following format:

    <name>:<nsets>:<bsize>:<assoc>:<rrpv_width>:<repl>

    <name>   - name of the cache being defined
    <nsets>  - number of sets in the cache
    <bsize>  - block size of the cache
    <assoc>  - associativity of the cache
    <rrpv_width> - width of ReReference Prediction Value register
    <repl>   - block replacement strategy, 'l'-LRU, 'f'-FIFO, 'r'-random 'a'-ARC 'b'-Bimodal RRIP 's'-Static RRIP 'd'-Dynamic RRIP

Eg of usage: for DRRIP
./Run.pl -db ./bench.db -dir results/gcc -benchmark gcc -sim ~/Cache_replacment/ss3/sim-cache -args " -max:inst 1000000000 -cache:il1 il1:2048:32:8:4:d"
Eg of usage: for ARC
./Run.pl -db ./bench.db -dir results/gcc -benchmark gcc -sim ~/Cache_replacment/ss3/sim-cache -args " -max:inst 1000000000 -cache:il1 il1:2048:32:8:4:a"

GitHub Repositry Details: https://github.com/cvsandeep/Cache_replacment.git

In some application DRRIP is better than ARC due to following reasons
  - ARC references the cache block as recent or frequently used entries where as DRRIP as more references as M is greater than 2
  - ARC is only Trash resistant where as DRRIP is both scan and Trash resistant.

In some other application with very Long acess patterns it may have -ve performance than LRU as with too long pattern it cannot scan to rereference that block in this case ARC can act well as it is having a ghost buffer. if the pattern is too long ARC also will have -ve impact.
