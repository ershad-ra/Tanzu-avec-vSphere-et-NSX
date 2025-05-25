# ☸️ Déploiement d'une Application 4-Tiers sur une Infrastructure Tanzu Kubernetes Grid (TKG)

Ce document présente les étapes techniques réalisées dans un environnement vSphere avec Tanzu, pour la mise en place d’une application multi-tier de test (`Yelb`) sur deux modes : **TKG zonal** et **vSphere Pods**.

---

## 🧱 Infrastructure mise en place

- ✅ **Supervisor Cluster** activé (Workload Management)
- ✅ **Deux clusters vSphere** :
  - `Cluster-MGMT` : pour Aria et le management
  - `Cluster-COMP` : hébergeant les workloads TKG
- ✅ **Un cluster TKG zonal** : `tkg-cluster01` (3 nœuds)
- ✅ **vSphere Distributed Switch (VDS)** utilisé
- ✅ **Pas de NSX ALB**, mais **NSX-T installé**
- ✅ **Stockage partagé SAN iSCSI**
- ✅ **Content Library** configurée
- ✅ **Aria Automation et Aria Operations** intégrés

---

## 🧩 Application déployée : **Yelb**

**Yelb** est une application 4-tiers composée de :
- `yelb-ui` (interface web)
- `yelb-appserver` (backend)
- `yelb-db` (PostgreSQL)
- `redis-server`

Elle a été déployée selon **2 scénarios** :

### 1. Dans un **namespace Supervisor** (vSphere Pods)
- Namespace : `yelb`
- Utilise des **vSphere Pods** (micro-VMs créées par le vSpherelet)

### 2. Dans un **cluster TKG zonal**
- Namespace : `app-01`
- Déploiement classique Kubernetes via YAML
- LoadBalancer configuré pour exposer l’UI

---

## 🔐 Conformité avec la politique de sécurité `restricted`

Tous les manifests YAML ont été adaptés pour respecter :
- `runAsNonRoot: true`
- `seccompProfile: RuntimeDefault`
- `allowPrivilegeEscalation: false`
- `capabilities.drop: ["ALL"]`

---

## 🔎 Déploiement et validation

### 🔹 Connexion au cluster TKG :

```bash
kubectl-vsphere login \
  --server https://<IP-WCP> \
  --vsphere-username administrator@cloudnex.fr \
  --tanzu-kubernetes-cluster-name tkg-cluster01 \
  --tanzu-kubernetes-cluster-namespace app-01 \
  --insecure-skip-tls-verify

kubectl config use-context tkg-cluster01
