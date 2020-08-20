# Notes

10/20/2020

- Operations Orchestration: solo para VMs, no para servidores físicos
- Si el servidor virtual tiene más de 400GB, **NO** se toma snapshot
- Los snapshots se mantienen solamente dos días
- Reboot: es un cambio de estado del servidor. Necesita Change Request
- `locate ps_mon.log` - normalmente en /var/log/OV/log/OpC/ps_mon.log
- `locate ps_mon.cfg` - normalmente en /var/opt/OV/conf/OpC/ps_mon.cfg
- Cada 5 minutos corre el agente de monitoreo
- Parcheado virtual NO genera incidentes porque se suprime el ticket automáticamente el flow
- EVS: servidores físicos, administran los recursos. UNIX maneja el sistema operativo.

- Incidente: algo circunstancial
- Problema: incidente que se repite
