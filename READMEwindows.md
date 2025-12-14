# DHCP Lab — Windows Server (Scope + Reservation)

Mini-lab réalisé en VM pour démontrer la mise en place d’un serveur DHCP sous Windows Server :
- création d’une étendue IPv4
- distribution dynamique d’adresses
- réservation (IP fixe basée sur l’adresse MAC)
- vérifications côté clients

## Objectifs
- Déployer un rôle **DHCP Server** sur Windows Server
- Configurer un réseau `172.20.0.0/24`
- Créer une étendue DHCP `172.20.0.100 → 172.20.0.200`
- Réserver l’adresse `172.20.0.10` pour un client identifié par MAC

## Environnement
- Hyperviseur : VirtualBox
- Réseau : **Internal Network** `intnet`
- Serveur : Windows Server (VM) — `SRV-DHCP`
- Clients : Windows (VM) — Client 1 et Client 2

## Configuration réalisée

### Serveur DHCP
- Nom d’hôte : `SRV-DHCP`
- IP statique : `172.20.0.1/24`
- Rôle : DHCP Server installé + post-deployment configuration effectuée
- Étendue : `172.20.0.100` à `172.20.0.200` (réseau `172.20.0.0/24`)
- Réservation : IP `172.20.0.10` liée à la MAC du client réservé

### Clients
- Client 1 : obtient une IP dynamique dans l’étendue
- Client 2 : obtient **toujours** `172.20.0.10` via réservation, même après `release/renew`

## Preuves (captures)
1. **Scope DHCP (serveur)**  
   ![Scope DHCP](ressources/windows/01-dhcp-server-scope.png)

2. **Client 1 — DHCP dynamique**  
   ![Client 1](ressources/windows/02-client1-dhcp.png)

3. **Client 2 — IP réservée**  
   ![Client 2](ressources/windows/03-client2-reservation.png)

4. **Réservation côté serveur**  
   ![Reservation](ressources/windows/04-server-reservation.png)

## Tests effectués
Sur les clients :
```
ipconfig /release
ipconfig /renew
ipconfig /all
```