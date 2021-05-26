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
  
- #ifdef CS333_P2

int

getprocs(uint max, struct uproc* table)

{
  
  int i = 0;
  
  struct proc* p;
  
  acquire(&ptable.lock);
  
  if(!table || max <= 0){
    
    release(&ptable.lock);
    
    return -1;
  
  }
  
  for(p = ptable.proc;p < &ptable.proc[NPROC];p++){
    
    if(i >= max)
      
      break;
    
    if(p->state != EMBRYO && p->state != UNUSED){
      
      table[i].pid = p->pid;
      
      table[i].uid = p->uid;
      
      table[i].gid = p->gid;
      
      table[i].ppid = (!p->parent) ? p->pid:p->parent->pid;
      
      table[i].elapsed_ticks = ticks - p->start_ticks;
      
      table[i].CPU_total_ticks = p->cpu_ticks_total;
      
      table[i].size = p->sz;
      
      safestrcpy(table[i].state, states[p->state], sizeof(table[i]).state);
      
      safestrcpy(table[i].name, p->name, sizeof(table[i]).name);
      
      i++;
    
    }
  
  }
  
  release(&ptable.lock);
  
  return i;

}

#endif // CS333_P2

## proc.h(Line 55-60)

- #ifdef CS333_P1

    uint start_ticks;

  #endif
  
  #ifdef CS333_P2
  
    uint uid;
    
    uint gid;

    uint cpu_ticks_total;
    
    uint cpu_ticks_in;

   #endif

## syscall.c

- #ifdef CS333_P2
  
  extern int sys_getuid(void);
  
  extern int sys_getgid(void);
  
  extern int sys_getppid(void);
  
  extern int sys_setuid(void);
  
  extern int sys_setgid(void);

  extern int sys_getprocs(void);
  
  #endif
  
- #ifdef CS333_P1
  
  [SYS_date]    sys_date,
  
  #endif

- #ifdef CS333_P2

  [SYS_getuid]   sys_getuid,
  
  [SYS_getgid]   sys_getgid,
  
  [SYS_getppid]  sys_getppid,
   
  [SYS_setuid]   sys_setuid,
  
  [SYS_setgid]   sys_setgid,
  
  [SYS_getprocs] sys_getprocs,

  #endif // CS333_P2
  
- #ifdef CS333_P1
  
  [SYS_date]    "date",
  
  #endif

- #ifdef CS333_P2
  
  [SYS_getuid]  "getuid",
  
  [SYS_getgid]  "getgid",
  
  [SYS_getppid] "getppid",
  
  [SYS_setuid]  "setuid",
  
  [SYS_setgid]  "setgid",
  
  [SYS_getprocs]  "getprocs",
  
  #endif
  
## syscall.h

- #define SYS_date    SYS_halt+1
  
  #define SYS_getuid  SYS_date+1
  
  #define SYS_getgid  SYS_getuid+1
  
  #define SYS_getppid SYS_getgid+1
  
  #define SYS_setuid  SYS_getppid+1
  
  #define SYS_setgid  SYS_setuid+1
  
  #define SYS_getprocs  SYS_setgid+1
  
## sysproc.c
