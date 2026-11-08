# 🌐 Projet Réseau Multi-Sites : TechGlobal Solutions (Cisco Packet Tracer)

## 📝 Description du Projet
Ce projet consiste en la conception, la virtualisation et la sécurisation d'une infrastructure réseau d'entreprise multi-sites pour la société **TechGlobal Solutions**. 
L'objectif est de relier un Siège Social (Site A) à une Agence Distante (Site B) en utilisant des VLANs, du routage inter-VLAN (Router-on-a-Stick), du routage dynamique (OSPF), des services centralisés (DHCP/DNS/Web/FTP) et des listes de contrôle d'accès (ACL) pour sécuriser les flux.

## 🛠️ Technologies Utilisées
*   **Logiciel** : Cisco Packet Tracer
*   **Niveau 2** : VLANs (10, 20, 30, 40), Liens Trunk 802.1Q, Ports d'accès.
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
| WAN | Lien Inter-site | 10.0.0.0/30 | 10.0.0.0/30 | 10.0.0.1 | 10.0.0.2 |
| ISP | Vers Internet | 200.1.1.0/24 | - | 200.1.1.2 | - |

### 🖥️ Serveurs (Site A - VLAN 10)
*   **Serveur 1 (DHCP/DNS/Web)** : `192.168.10.10`
*   **Serveur 2 (FTP/Mail)** : `192.168.10.11`

## 🚀 Fonctionnalités Implémentées
1.  **Virtualisation L2** : Segmentation stricte des domaines de diffusion.
2.  **Routage Inter-site** : OSPFv2 assure la convergence rapide entre les deux sites.
3.  **Services Centralisés** : Le serveur DHCP du Site A distribue les adresses aux deux sites via DHCP Relay.
4.  **Accès Internet** : NAT/PAT configuré sur Router_A pour traduire les adresses privées vers l'IP publique.
5.  **Sécurité** :
    *   Le VLAN Guest (40) est isolé du réseau interne (sauf DNS).
    *   Le VLAN Finance (20) est protégé et accessible uniquement par Admin et IT.
    *   L'accès SSH aux routeurs est restreint au VLAN IT (30).

## 📂 Contenu du Dépôt
*   `TechGlobal_Solutions.pkt` : Le fichier de topologie Cisco Packet Tracer complet.
*   `README.md` : Ce fichier de documentation.
*   `Rapport_Technique.pdf` : (Optionnel) Le rapport détaillé du projet.
*   `Captures/` : (Optionnel) Dossier contenant les captures d'écran des tests de validation (DHCP, OSPF, ACLs).

## 🧪 Tests de Validation
*   **DHCP** : Les PC du Site B obtiennent une IP via le serveur du Site A.
*   **OSPF** : `show ip ospf neighbor` affiche l'état `FULL`.
*   **ACL Guest** : Ping vers Finance échoue, mais navigation Web (DNS) fonctionne.
*   **Internet** : Ping vers `8.8.8.8` réussi depuis un PC interne.

---
*Projet réalisé dans le cadre du module Réseaux Informatiques & Architecture LAN/WAN.*