
# InnoDB recovery


# Locks
```SQL
-- Mostra tots els processos bloquejats, és molt útil per entendre que està passant si els serveis que ataquen a la bbdd deixen de funcionar o bé degraden el seu comportament
show open tbales where in_use>0;

-- Solta un churro d'info que a priori és complicada de digerir. Pero en cas de recovery de la bbdd el chatgpt et pot dir en quin estat es troba l'innodb i salvarte bastant
show engine innodb status;
```
