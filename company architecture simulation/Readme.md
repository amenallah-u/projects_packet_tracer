# 🌐 Projet Réseau Multi-Sites : TechGlobal Solutions (Cisco Packet Tracer)

## 📝 Description du Projet
Ce projet académique consiste en la conception, la virtualisation et la sécurisation d'une infrastructure réseau d'entreprise multi-sites pour la société **TechGlobal Solutions**. 
L'objectif est de relier un Siège Social (Site A) à une Agence Distante (Site B) en utilisant des VLANs, du routage inter-VLAN (Router-on-a-Stick), du routage dynamique (OSPF), des services centralisés (DHCP/DNS/Web/FTP/Mail) et des listes de contrôle d'accès (ACL) pour sécuriser les flux.

**Réalisé dans le cadre du module :** Virtualisation Réseau
**Sous la supervision de :** Professeur Bilel Hamdi

## 🛠️ Technologies Utilisées
*   **Logiciel** : Cisco Packet Tracer
*   **Niveau 2** : VLANs (10, 20, 30, 40, 50), Liens Trunk 802.1Q, Ports d'accès.
*   **Niveau 3** : Router-on-a-Stick, Routage dynamique OSPFv2, Routage statique (par défaut), NAT/PAT.
*   **Services Réseaux** : DHCP centralisé (avec relais `ip helper-address`), DNS, HTTP (Intranet), FTP, Messagerie.
*   **Sécurité** : ACLs étendues (Isolation des invités, Protection de la Finance, Restriction SSH).

## 🗺️ Plan d'Adressage IP

| VLAN | Nom | Site A | Site B | Passerelle A | Passerelle B |
|------|-----|--------|--------|--------------|--------------|
| 10 | Administration | 192.168.10.0/24 | 192.168.110.0/24 | 192.168.10.1 | 192.168.110.1 |
| 20 | Finance | 192.168.20.0/24 | 192.168.120.0/24 | 192.168.20.1 | 192.168.120.1 |
| 30 | IT | 192.168.30.0/24 | - | 192.168.30.1 | - |
| 40 | Guest | 192.168.40.0/24 | 192.168.140.0/24 | 192.168.40.1 | 192.168.140.1 |
| 50 | Data Center 2 | 192.168.50.0/24 | - | 192.168.50.1 | - |
| WAN | Lien Inter-site | 10.0.0.0/30 | 10.0.0.0/30 | 10.0.0.1 | 10.0.0.2 |
| ISP | Vers Internet | 200.1.1.0/24 | - | 200.1.1.2 | - |

### 🖥️ Architecture des Data Centers (Site A)

**1. Data Center 1 (VLAN 10 - Administration)**
Ce zone contient les serveurs d'infrastructure critiques avec des adresses IP statiques :
*   **Serveur 1 (192.168.10.10)** : DHCP, DNS, Web (Intranet)
*   **Serveur 2 (192.168.10.11)** : FTP, Messagerie (Mail)

**2. Data Center 2 (VLAN 50)**
Cette zone contient deux serveurs clients qui reçoivent leurs adresses IP **dynamiquement** via le serveur DHCP du Data Center 1.

## 🚀 Fonctionnalités Implémentées
1.  **Virtualisation L2** : Segmentation stricte des domaines de diffusion (5 VLANs).
2.  **Routage Inter-site** : OSPFv2 assure la convergence rapide entre les deux sites.
3.  **Services Centralisés** : Le serveur DHCP (DC1) distribue les adresses aux deux sites et au Data Center 2 via DHCP Relay.
4.  **Accès Internet** : NAT/PAT configuré sur Router_A pour traduire les adresses privées vers l'IP publique.
5.  **Sécurité** :
    *   Le VLAN Guest (40) est isolé du réseau interne (seul le DNS est autorisé).
    *   Le VLAN Finance (20) est protégé et accessible uniquement par Admin et IT.
    *   L'accès SSH aux routeurs est restreint au VLAN IT (30).

## 📂 Contenu du Dépôt
*   `TechGlobal_Solutions.pkt` : Le fichier de topologie Cisco Packet Tracer complet.
*   `README.md` : Ce fichier de documentation.
*   `Rapport_Technique.pdf` : Le rapport détaillé du projet.
*   `Captures/` : Dossier contenant les captures d'écran des tests de validation.
*   `Configurations/` : Contient les configuration des equipments reseau utilise.

## 🧪 Tests de Validation
*   **DHCP (Site B)** : Les PC du Site B obtiennent une IP via le serveur du Site A (`ip helper-address`).
*   **DHCP (Data Center 2)** : Les serveurs du VLAN 50 obtiennent une IP dynamiquement.
*   **OSPF** : `show ip ospf neighbor` affiche l'état `FULL` entre Router_A et Router_B.
*   **ACL Guest** : Ping vers Finance échoue, mais navigation Web (`www.techglobal.lan`) fonctionne.
*   **Internet** : Ping vers `8.8.8.8` réussi depuis un PC interne (via NAT).
*   **Services** : Connexion FTP réussie et envoi/réception de mail validés.

---
*Projet académique (institut: isikef) réalisé dans le cadre du module Virtualisation Réseau - Sous la supervision du Professeur Bilel Hamdi.*