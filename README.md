# nfs-docker
Script to manage Docker-based NFS server services with VLAN separation

Ez a program a Docker alapu NFS szolgaltatas kezeleshez nyujt segitseget


# Keszitette: Dobo Csaba, dobocs@invitech.hu
# utoljara frissitve: 2016.szept.22.


# Funkciok:
#  (1) Szabad tarterulet ellenorzese (zfs get -o value -Hp available pool1)
#  (2) Szabad VLAN ID ellenorzese (ovs-vsctl list-br)
#  (3) Szolgaltasnev ellenorzese (/adatok mappaban levo almappa nevei)


#  (4) Kert nevvel uj mappa felvetele
#  (5) Uj zfs keszites zfs create pool1/szolgaltatasnev
#  (6) A letrehozott zfs felcsatolasa zfs set mountpoint=/adatok/szolgaltatasnev pool1/szolgaltatasnev
#  (7) Quota meghatarozasa (mekkkora teruletre van szukseg) zfs set quota=5G pool1/szolgaltatasnev
#  (8) Uj fake bridge felvetele: ovs-vsctl add-br ovsbr1.100 ovsbr1 100 (az ID = a korabban eldontott szam)
#  (9) Az uj bridge bekapcsolasa. ifconfig ovsbr1.101 up
# (10) docker kontener inditas: docker run -d --privileged --name szolgnev -v /adatok/szolgnev:/exports/foo nfs-invitel /exports/foo# (11) docker es bridge osszekapcsolasa: ./pipework ovsbr1.100 <docker nev v ID> 192.168.12.11/24
