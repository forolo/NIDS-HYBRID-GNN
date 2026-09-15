# 🛡️ NIDS-HYBRID-GNN : Détection d'Intrusions Réseau Hybride, Explicable et Auto-Supervisée

> **Projet de Master 2 — Sécurité Informatique**  
> Architecture hybride associant **E-GraphSAGE** (GNN avec attributs d'arêtes), **Graph Contrastive Learning (GCL)** et **XGBoost** pour la détection d'intrusions sur graphes réseau dynamiques non-euclidiens.

---

## 📋 Table des Matières
1. [Aperçu de l'Architecture](#-aperçu-de-larchitecture)
2. [Préréquis Système & Matériel](#-prérequis-système--matériel)
3. [Procédure d'Installation Pas à Pas](#-procédure-dinstallation-pas-à-pas)
4. [Reproduction des Expérimentations](#-reproduction-des-expérimentations)
5. [Déploiement en Production (Docker & FastAPI)](#-déploiement-en-production-docker--fastapi)
6. [Guide de l'API REST](#-guide-de-lapi-rest)
7. [Explicabilité Duale (SHAP & GNNExplainer)](#-explicabilité-duale-shap--gnnexplainer)

---

## 🏗️ Aperçu de l'Architecture

Le pipeline suit une approche à trois étages :
1. **Graphes Temporels Dynamiques :** Structuration du trafic ($G_t = (V_t, E_t)$) à partir de flux réseau (PCAP / NetFlow). Les hôtes sont des nœuds, les flux sont des arêtes orientées munies d'attributs $E_{feat}$ (durée, octets, flags TCP).
2. **Encodeur Topologique (E-GraphSAGE + GCL) :** Génération d'embeddings denses $Z_v$ par passage de messages inductif pré-entraîné de manière auto-supervisée (InfoNCE loss).
3. **Classifieur & Explicabilité Duale :** Classification des menaces par XGBoost avec justifications locales (TreeSHAP) et structurelles (GNNExplainer).

---

## 💻 Prérequis Système & Matériel

### Configuration Minimale (Inférence / Test local)
* **OS :** Windows 11 Pro / Ubuntu 22.04 LTS / Debian 11
* **CPU :** Intel Core i7 / AMD Ryzen 7 (8 cœurs)
* **RAM :** 16 GB
* **GPU :** NVIDIA GPU (DirectX 12 / CUDA compatible), min 4 GB VRAM (ex: NVIDIA RTX A1000 Laptop GPU)

### Configuration Recommandée (Entraînement complet)
* **RAM :** 32 GB
* **GPU :** NVIDIA V100 / A100 ou RTX Series avec 6 GB+ VRAM
* **Drivers :** NVIDIA Driver >= 525.x, CUDA Toolkit 11.8 ou 12.1

---

## 🛠️ Procédure d'Installation Pas à Pas

### Étape 1 : Cloner le Dépôt
```bash
git clone [https://github.com/votre-org/nids-hybrid-gnn.git](https://github.com/votre-org/nids-hybrid-gnn.git)
cd nids-hybrid-gnn
