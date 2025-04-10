**"Tanzu avec vSphere et NSX"** :

---

### **Nom du projet :**
**Déploiement de Tanzu avec vSphere et NSX**

---

### **Objectifs du projet :**
- Mettre en place une infrastructure **multi-cluster Tanzu**.
- Intégrer Tanzu à la solution **SDN NSX**.
- Activer les fonctionnalités **Kubernetes de base** : services `ClusterIP`, `Ingress`, etc.
- Déployer une **application 3-tiers** sur Tanzu (avec ou sans automatisation).
- Appliquer des **politiques réseau (Network Policies)** à l’aide de NSX pour renforcer la sécurité.

---

### **Plan du projet :**

#### **Phase 1 : Conception de l’architecture Système et Réseau**
- Définir le **nombre de serveurs** physiques et leur répartition entre :
  - Cluster **Compute**
  - Cluster **Management**
- Définir les **sous-réseaux** :
  - Management
  - VM / Workloads
  - Overlay (TEP)
  - Frontend / Backend si nécessaire
- Identifier les **nœuds à intégrer dans NSX** et les **zones de transport** correspondantes.
- Valider les **pré-requis techniques Tanzu** (versions, compatibilité, ressources).
- Élaborer un **schéma d’architecture** global.

#### **Phase 2 : Déploiement de l’infrastructure Système**
- Installation et configuration des **hôtes ESXi**.
- Installation et configuration de **vCenter Server**.
- Ajout des hôtes ESXi aux clusters.
- Installation de **NSX Manager** et configuration initiale.
- Enregistrement de NSX avec vCenter.

#### **Phase 3 : Préparation de l'infrastructure SDN pour Tanzu**
- Création et configuration des **transport zones** NSX.
- Configuration des **TEP** (Tunnel Endpoints) sur les nœuds ESXi.
- Déploiement et configuration des **edge nodes NSX**.
- Création des **segments NSX** pour Tanzu (overlay, frontend/backend, etc.).
- Création des **Tier-0/Tier-1 gateways** si nécessaires.

#### **Phase 4 : Installation et configuration de Tanzu**
- Activation de **Workload Management** via vCenter.
- Déploiement du **cluster de management Tanzu**.
- Configuration des **supervisors**.
- Intégration avec **NSX-T** pour la gestion réseau de Tanzu.

#### **Phase 5 : Configuration et test des fonctionnalités Kubernetes**
- Création de **namespaces Kubernetes**.
- Déploiement de services de type :
  - `ClusterIP`
  - `LoadBalancer` (via NSX)
  - `Ingress` (via Contour, ou autre Ingress Controller)
- Tests de connectivité entre les pods et services.

#### **Phase 6 : Déploiement de l’application 3-tiers**
- Déploiement des composants **frontend**, **backend** et **base de données** dans Kubernetes.
- Utilisation de YAML ou **automatisation via Helm/Tanzu Application Platform (TAP)**.
- Validation du bon fonctionnement de bout en bout de l’application.

#### **Phase 7 : Sécurité et Network Policies**
- Création de **Network Policies Kubernetes**.
- Application et validation de la segmentation réseau via **NSX**.
- Test des restrictions d’accès inter-services.

#### **Phase 8 : Documentation et préparation de la présentation**
- Rédaction d’une **documentation technique** du projet.
- Création d’un **diaporama de présentation** pour restituer le projet.
- Préparation à la **démonstration finale**.