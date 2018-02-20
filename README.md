# RIPproject
Скударнова Анастасия. ФТ-201. n = 16
- 1.	Собрала сеть как на картинке. Для решения проблемы нехватки портов в роутерах подключила плату NM-2FE2W. Настроила IP адреса на компьютерах PC1,  PC2 и серверах
---
- 2.	Настраивала IP адреса на портах роутеров:


###### Router 1

> Router>enable  
> Router#conf t  
> Router(config)#int fa1/0  
> Router(config-if)#ip address 192.168.1.1 255.255.255.0  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

> Router(config)#int fa0/1  
> Router(config-if)#ip address 10.16.1.1 255.255.255.0  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

> Router(config)#int fa0/0  
> Router(config-if)#ip address 192.168.10.1 255.255.255.252  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

###### Router 2

> Router>enable  
> Router#conf t  
> Router(config)#int fa 1/0  
> Router(config-if)#ip address 192.168.2.1 255.255.255.0  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

> Router(config)#int fa 0/0  
> Router(config-if)#ip address 192.168.10.2 255.255.255.252  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

> Router(config)#int fa 0/1  
> Router(config-if)#ip address 192.168.10.6 255.255.255.252  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  
> Router(config)#  

###### Router 3

> Router>enable  
> Router#conf t  
> Router(config)#int fa 0/1  
> Router(config-if)#ip address 192.168.10.5 255.255.255.252  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

> Router(config)#int fa 0/0  
> Router(config-if)#ip address 10.16.1.2 255.255.255.0  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  

> Router(config)#int fa 1/0  
> Router(config-if)#ip address 192.168.3.1 255.255.255.0  
> Router(config-if)#no shutdown  
> Router(config-if)#exit  
> Router(config)#  
> Router#  
---
- 3.	В качестве шлюза по умолчанию для PC0 и PC1 установила Router 1 (n – четное), для серверов – ближайший к ним роутер.
---
- 4.	Настроила RIP на роутерах:

###### Router 1

> Router>enable  
> Router#conf t  
> Router(config)#router rip  
> Router(config-router)#network 10.16.1.0  
> Router(config-router)#network 192.168.10.0  
> Router(config-router)#network 192.168.1.0  
> Router(config-router)#exit  
> Router(config)#  
> Router#  

###### Router 2

> Router>enable  
> Router#conf t  
> Router(config)#router rip  
> Router(config-router)#network 192.168.10.4  
> Router(config-router)#network 192.168.10.0  
> Router(config-router)#network 192.168.2.0  
> Router(config-router)#exit  
> Router(config)#  

###### Router 3

> Router>enable  
> Router#conf t  
> Router(config)#router rip  
> Router(config-router)#network 192.168.3.0  
> Router(config-router)#network 192.168.10.4  
> Router(config-router)#network 10.16.1.2  
> Router(config-router)#exit  
> Router(config)#   

Ping полностью работает между всеми, но 3 сервер всегда теряет первый пакет в не зависимости от получателя (в обратную сторону потерь нет).
