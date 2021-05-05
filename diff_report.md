<<<<<<< HEAD
# Code Modification

Kode Yang diubah dalam XV6

## Makefile (Line 3,4,16)

- CS333_PROJECT ?= 1
- PRINT_SYSCALLS ?= 1

- CS333_UPROGS += _date

## Syscall.c (Line 109-112,139-141, 182-185)

- #ifdef CS333_P1
 
  extern int sys_date(void);
  
  #endif
  
- #ifdef CS333_P1
 
  [SYS_date] sys_date,
  
  #endif

- #ifdef PRINT_SYSCALLS

    cprintf("%s -> %d\n",
    
     syscallnames[num], curproc->tf->eax);
         
  #endif
  
## user.h (Line 28-30)
- #ifdef CS333_P1
  
  int date(struct rtcdate*);
    
  #endif // CS333_P1
  
## usys.s (Line 33)
- SYSCALL(date)

## syscall.h (Line 24)
- #define SYS_date    SYS_halt+1

## sysproc.c (Line 101-111)
- #ifdef CS333_P1

   int
   
   sys_date(void)
   
   {
   
     struct rtcdate *d;
     
     if(argptr(0,(void*)&d, sizeof(struct rtcdate))<0)
     
       return -1;
       
     cmostime(d);
     
     return 0;
   
   }
   
   #endif

## proc.h (Line 52-54)
- #ifdef CS333_P1

  uint start_ticks;
  
  #endif // CS333_P1
  
## proc.c (Line 151-153, 569-575)
- #ifdef CS333_P1

  p->start_ticks = ticks;
  
  #endif
  
-  #ifdef CS333_P1

    uint elapsed_in_ms = ticks - p->start_ticks;
    
    uint elapsed_in_sec = elapsed_in_ms / 1000;
    
    uint elapsed_decimal = elapsed_in_ms % 1000;
    
    cprintf("%d\t%s\t\t%d.%d\t%s\t%d\t", p->pid, p->name, elapsed_in_sec, elapsed_decimal, state_string, p->sz);
    
  #endif // CS333_P1
=======
# Code Modification

Kode Yang diubah dalam XV6

## Makefile (Line 3,4,16)

- CS333_PROJECT ?= 1
- PRINT_SYSCALLS ?= 1

- CS333_UPROGS += _date

## Syscall.c (Line 109-112,139-141, 182-185)

- #ifdef CS333_P1
 
  extern int sys_date(void);
  
  #endif
  
- #ifdef CS333_P1
 
  [SYS_date] sys_date,
  
  #endif

- #ifdef PRINT_SYSCALLS

    cprintf("%s -> %d\n",
    
     syscallnames[num], curproc->tf->eax);
         
  #endif
  
## user.h (Line 28-30)
- #ifdef CS333_P1
  
  int date(struct rtcdate*);
    
  #endif // CS333_P1
  
## usys.s (Line 33)
- SYSCALL(date)

## syscall.h (Line 24)
- #define SYS_date    SYS_halt+1

## sysproc.c (Line 101-111)
- #ifdef CS333_P1

   int
   
   sys_date(void)
   
   {
   
     struct rtcdate *d;
     
     if(argptr(0,(void*)&d, sizeof(struct rtcdate))<0)
     
       return -1;
       
     cmostime(d);
     
     return 0;
   
   }
   
   #endif

## proc.h (Line 52-54)
- #ifdef CS333_P1

  uint start_ticks;
  
  #endif // CS333_P1
  
## proc.c (Line 151-153, 569-575)
- #ifdef CS333_P1

  p->start_ticks = ticks;
  
  #endif
  
-  #ifdef CS333_P1

    uint elapsed_in_ms = ticks - p->start_ticks;
    
    uint elapsed_in_sec = elapsed_in_ms / 1000;
    
    uint elapsed_decimal = elapsed_in_ms % 1000;
    
    cprintf("%d\t%s\t\t%d.%d\t%s\t%d\t", p->pid, p->name, elapsed_in_sec, elapsed_decimal, state_string, p->sz);
    
  #endif // CS333_P1
>>>>>>> a8073d39a89f4cd87755ed4de5528dd0831fce61
