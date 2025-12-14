# DHCP Server – Debian (isc-dhcp-server)

## 🎯 Objectif
Mettre en place un **serveur DHCP fonctionnel sous Debian** capable :
- d’attribuer automatiquement des adresses IP à des clients
- de gérer une **plage d’adresses DHCP**
- de configurer une **réservation d’adresse IP par adresse MAC**

Ce laboratoire a été réalisé dans un environnement virtualisé et vise à démontrer des compétences concrètes en **administration systèmes et réseaux (Linux)**.

---

## 🧱 Architecture du lab

- **Serveur DHCP**
  - OS : Debian (serveur)
  - Rôle : DHCP (isc-dhcp-server)
  - Interface LAN : `enp0s8`
  - IP statique : `172.20.0.1/24`

- **Réseau**
  - Type : Réseau interne (VirtualBox)
  - Plage réseau : `172.20.0.0/24`
  - Étendue DHCP : `172.20.0.80 → 172.20.0.150`

- **Clients**
  - Client 1 : DHCP dynamique
  - Client 2 : DHCP avec réservation par MAC

---

## ⚙️ Installation du service DHCP

```bash
sudo apt update
sudo apt install isc-dhcp-server
# DHCP Lab — Debian Server (isc-dhcp-server)

Mini-lab réalisé en VM pour démontrer la mise en place d’un serveur **DHCP sous Debian** :
- configuration du service `isc-dhcp-server`
- distribution dynamique d’adresses IPv4
- réservation d’adresse IP basée sur l’adresse MAC
- vérifications côté clients

## Objectifs
- Installer et configurer un serveur **DHCP sous Debian**
- Configurer un réseau `172.20.0.0/24`
- Créer une étendue DHCP `172.20.0.80 → 172.20.0.150`
- Réserver l’adresse `172.20.0.100` pour un client identifié par MAC

## Environnement
- Hyperviseur : VirtualBox
- Réseau : **Internal Network** `intnet`
- Serveur : Debian Server (VM) — `SRVLX01`
- Clients : Linux (VM) — Client 1 et Client 2

## Configuration réalisée

### Serveur DHCP
- Nom d’hôte : `SRVLX01`
- IP statique (LAN) : `172.20.0.1/24`
- Service : `isc-dhcp-server`
- Interface d’écoute DHCP : `enp0s8`
- Réseau : `172.20.0.0/24`
- Étendue DHCP : `172.20.0.80` à `172.20.0.150`
- Réservation : IP `172.20.0.100` liée à l’adresse MAC du client réservé

### Clients
- Client 1 : obtient une IP dynamique dans la plage DHCP
- Client 2 : obtient **toujours** l’adresse `172.20.0.100` via réservation DHCP

## Preuves (captures)

1. **Serveur DHCP Debian — service actif**  
   ![DHCP Server](ressources/debian/srv-dhcp-status.png)

2. **Client 1 — DHCP dynamique**  
   ![Client 1 DHCP](ressources/debian/client1-dhcp.png)

3. **Client 2 — IP réservée**  
   ![Client 2 Reservation](ressources/debian/client2-reservation.png)

4. **Réservation DHCP côté serveur**  
   ![DHCP Reservation](ressources/debian/reservation-server.png)

