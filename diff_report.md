# Code Modification

Kode Yang diubah dalam XV6

## Makefile (Line 3)

- CS333_PROJECT ?= 2

## defs.h (Line 12-15,130-132)

- #ifdef CS333_P2
  
  struct uproc;

  #endif // CS333_P2

- #ifdef CS333_P2

  int             getprocs(uint max, struct uproc* table);
  
  #endif // CS333_P2
  
## param.h(Line 18-20)

- #ifdef CS333_P2
  
  #define DEFAULTID     0  // default ID for UID/GID of process
 
  #endif // CS333_P2
  
## proc.c

- #ifdef CS333_P2

  #include "uproc.h"
  
  #endif //CS333_P2

- #ifdef CS333_P2
  
    p->cpu_ticks_total = 0;
  
    p->cpu_ticks_in = 0;
  
  #endif // CS333_P2

- #ifdef CS333_P2
  
    p->uid = DEFAULT_UID;
   
    p->gid = DEFAULT_GID;
  
  #endif
  
- #ifdef CS333_P2
  
    np->uid = curproc->uid;
  
    np->gid = curproc->gid;
  
  #endif // CS333_P2
  
- #ifdef CS333_P2
  
    p->cpu_ticks_in = ticks;
  
  #endif // CS333_P2
  
- #ifdef CS333_P2
 
    p->cpu_ticks_total += ticks - p->cpu_ticks_in;
  
  #endif // CS333_P2
  
- #if defined(CS333_P2)
  
  void

  procdumpP2P3P4(struct proc *p, char *state_string)
  
  {
    
    // cprintf("TODO for Project 2, delete this line and implement procdumpP2P3P4() in proc.c to print a row\n");
    
    int elapsed = ticks - p->start_ticks;
    
    uint elapsed_sec = elapsed / 1000;
    
    uint elapsed_mod = elapsed % 1000;
    
    int total = p->cpu_ticks_total;
    
    int total_sec = total/1000;
    
    int total_mod = total%1000;
    
    int ppid;
    
    if(p->parent)
    
    {
      
      ppid = p->parent->pid;
    
    }
    
    else
    
    {
    
      ppid = p->pid;
    
    }
    
    cprintf("%d\t%s\t\t%d\t%d\t%d\t%d.%d\t%d.%d\t%s\t%d\t", p->pid, p->name, p->uid, p->gid, ppid, elapsed_sec, elapsed_mod, total_sec, total_mod, state_string, p->sz);
    
    return;
  
  }
