
CENÁRIO
---
<! Laboratório Realizado em Ambiente Controlado para Fins de Estudo !>

![image](https://user-images.githubusercontent.com/111648247/208739596-b5e8da3f-4c60-42da-9e30-a51b0a4f918b.png)

**Config. Workstation Attacker [Hardware]**
```
[vagrant@srv-attacker-in ~]$ hostnamectl
   Static hostname: srv-attacker-in
         Icon name: computer-vm
           Chassis: vm
        Machine ID: <!output omitted!>
           Boot ID: <!output omitted!>
    Virtualization: vmware
  Operating System: CentOS Linux 7 (Core)
       CPE OS Name: cpe:/o:centos:centos:7
            Kernel: Linux 3.10.0-1127.el7.x86_64
      Architecture: x86-64
[vagrant@srv-attacker-in ~]$
-- Todos as maquinas tem o mesmo hardware e OS, divergindo apenas os pacotes instalados.
```

Credenciais
User: vagrant
Password: vagrant
Obs.: Ajuste ja realizado para ssh no arquivo "provision"


**Firewall Fortigate [Firmware / FortiOS]**
```
FortiGate-VM64 # get system status | grep [vV]*ersion
Version: FortiGate-VM64 v7.2.0,build1157,220331 (GA.F)
Release Version Information: GA
```

Pacotes & Repositórios Instalados
---
Repo Epel-release / Git / Medusa [Brute Force]
```
# yum install -y epel-release git wget tcpdump python3 vim tree nmap medusa
```

Base de Users and Passwords
https://github.com/duyet/bruteforce-database
```
$ git clone https://github.com/duyet/bruteforce-database
```

Sintaxe Attack
---
Cmd SRC Outside [Public IP 192.168.15.140 p 2022]
```
# medusa -h 192.168.15.140 -U /home/<!you_user!>/bruteforce-database/38650-username-sktorrent.txt -P /home/<!you_user!>/bruteforce-database/38650-password-sktorrent.txt -M ssh -n 2022
```

Cmd SRC Inside [Inside IP 10.100.0.20 p 22]
```
# medusa -h 10.100.0.20 -U /home/<!you_user!>/Documents/bruteforce-database/38650-username-sktorrent.txt -P /home/<!you_user!>/Documents/bruteforce-database/38650-password-sktorrent.txt -M ssh -n 22
```

Fonte para utilização "Medusa"

https://medium.com/@murilothink/realizando-ataque-de-brute-force-ssh-e-ftp-com-a-ferramenta-medusa-f6bd44b5bf53


Configuração IPS Fortigate
---

![image](https://user-images.githubusercontent.com/111648247/208739685-902fb56b-f425-4f02-ad16-49cd7ae923d1.png)

Security Profile > Intrusion Prevention > Create New Profile

![image](https://user-images.githubusercontent.com/111648247/208739716-0d60f40c-b41f-4d23-83dd-f1c13540cc97.png)

![image](https://user-images.githubusercontent.com/111648247/208739742-6a22967a-b9da-4374-90a3-259dcf579e8e.png)

Nesse caso foi editado e definido para detectar o ataque a cada três tentativas. 
Reforçando para customizar o "threshold" se faz necessário selecionar "signature".


Log & Reports
---

![image](https://user-images.githubusercontent.com/111648247/208739539-bfaa0dc9-767c-4a97-91a2-4aa63bfa3526.png)

Para ver o IPS em operação basta seguir o caminho: Log & Report > Security Events > Intrusion Prevention
Reforçando que ele esta apenas "detected" pois assim definimos, para bloquear bastar tirar de "Monitor" para "Block"
