# **Installation Guide**
https://www.debian.org/index.fr.html

1. Télécharger Oracle VM VirtualBox Manager dans Managed Sofware Center
2. Télécharger le fichier Debian 
3. Dans Oracle : New → 1020mb, Fixe, 30.8GB, Debian 64. Linux
4. Setting → Mettre le disque virutel de Debian
5. Start
6. English, Canada, Multilingual ( wait )
7. Hostname : ur_hostname
8. Domain : (vide)
9. Root PW (12) : ******
10. User : ur name
11. User PW (12) : ******
12. (wait)
13. MANUAL→SCSIX(0,0,0( (sda . . .)) →yes →PRI 30G free space →New part (CRANP next)→ 
14. SDA-30.8G
15. sda1-500m
16. sda2-1K-part
17. sda5-30.3G-part
18. sda5_crypt-30.3G-crypt
19. LVMGroup-root-10G /
20. LVMGroup-swap-2.3G swap
21. LVMGroup-home-5G home
22. LVMGroup-var-3G var
23. LVMGroup-srv-3G srv
24. LVMGroup-tmp-3G tmp
25. LVMGroup-var- - log-4G /var/log
26. sr0-1024M -rom
27. Cryp PW : ******
