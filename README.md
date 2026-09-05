<div align="center">

**Étudiant en master 2 [Informatique, Synthèse d'Images et Conception Graphique (ISICG)](https://www.sciences.unilim.fr/informatique/master-informatique-isicg/)**  
*Université de Limoges*

Intéressé par le **rendu PBR (Physically Based Rendering)**, la **simulation physique** et le **calcul accéléré sur GPU**.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/haroun-jilani-823a19321/) [![Email](https://img.shields.io/badge/Email-D14836?logo=gmail&logoColor=white)](mailto:haroun.jilani@etu.unilim.fr)

---
### 💻 Stack Technique
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=flat&logo=c%2B%2B&logoColor=white) ![C](https://img.shields.io/badge/c-%2300599C.svg?style=flat&logo=c&logoColor=white) ![Python](https://img.shields.io/badge/python-3670A0?style=flat&logo=python&logoColor=ffdd54) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=flat&logo=openjdk&logoColor=white)  
![CUDA](https://img.shields.io/badge/cuda-000000.svg?style=flat&logo=nVIDIA&logoColor=green) ![OpenMPI](https://img.shields.io/badge/Open%20MPI-%23313131.svg?style=flat) ![OpenMP](https://img.shields.io/badge/OpenMP-%23313131.svg?style=flat) ![OpenGL](https://img.shields.io/badge/OpenGL-%23FFFFFF.svg?style=flat&logo=opengl)  
![Git](https://img.shields.io/badge/Git-%23F05032.svg?style=flat&logo=git&logoColor=white) ![LaTeX](https://img.shields.io/badge/LaTeX-%23008080.svg?style=flat&logo=latex&logoColor=white)
</div>

<br>

# 🛠️ Projets

## 🌊 Simulation de fluides accélérée par GPU
**Stage R&D, laboratoire XLIM, Limoges**

Développement d'une simulation de fluides basée sur la méthode de Boltzmann (LBM), avec accélération GPU via CUDA. Le système prend en charge la simulation monophasique (1 fluide) puis diphasique (eau et air), modélisant la formation et la remontée de bulles d'air en 2D, avant une extension en 3D.

**Technologies :** 
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=flat&logo=c%2B%2B&logoColor=white) ![CUDA](https://img.shields.io/badge/cuda-000000.svg?style=flat&logo=nVIDIA&logoColor=green) ![Python](https://img.shields.io/badge/python-3670A0?style=flat&logo=python&logoColor=ffdd54) ![OpenGL](https://img.shields.io/badge/OpenGL-%23FFFFFF.svg?style=flat&logo=opengl) ![OpenVDB](https://img.shields.io/badge/OpenVDB-%23013243.svg?style=flat) ![NVIDIA Warp](https://img.shields.io/badge/NVIDIA%20Warp-%2376B900.svg?style=flat&logo=nvidia&logoColor=white)

### 1. Première phase : validation CPU vs GPU (1 fluide)
Implémentation initiale en Python pour valider la méthode LBM avant la parallélisation sur GPU. La simulation est visualisée avec OpenGL, en utilisant le cas test du vortex de von Kármán pour observer le comportement du fluide.

<table align="center" width="100%">
<tr>
<td align="center" width="50%">
<b>Implémentation Initiale (Python CPU)</b><br><br>
<video src="https://github.com/user-attachments/assets/f975a769-a7b0-4f14-ab77-7f287e923454" controls width="100%"></video>
<br><em>Résolution : 100 × 50 | ~143 ms/frame (~7 FPS) </em>
</td>
<td align="center" width="50%">
<b>Implémentation Optimisée (CUDA GPU)</b><br><br>
<video src="https://github.com/user-attachments/assets/0f347854-f7cf-4039-b175-759d79996c81" controls width="100%"></video>
<br><em>Résolution : 1200 × 800 | ~10 ms/frame (~100 FPS) </em>
</td>
</tr>
</table>

### 2. Deuxième phase : simulation diphasique (eau/air)
Extension du modèle pour simuler l'interaction entre deux fluides et la dynamique des bulles. Sur CPU, l'identification des composantes connexes (bulles) reposait sur un algorithme séquentiel itératif de type Union-Find sur grille. La parallélisation de cette réduction de graphe constituant un goulot d'étranglement, le calcul a été déporté sur GPU en intégrant l'algorithme optimisé CCL HA4 de NVIDIA, permettant un suivi précis en temps réel.

<table align="center" width="100%">
<tr>
<td align="center" width="50%">
<video src="https://github.com/user-attachments/assets/7afd0810-3702-48fb-98c2-70f209794d57" controls width="100%"></video>
<br><em>Simulation des fluides dans une structure poreuse 2D (céramique).</em>
</td>
<td align="center" width="50%">
<video src="https://github.com/user-attachments/assets/38f8e28f-ce1e-4e03-ac72-46dac5202c3d" controls width="100%"></video>
<br><em>Simulation diphasique d'un robinet illustrant la formation de bulles.</em>
</td>
</tr>
</table>

### 3. Simulation 3D et rendu volumétrique
Extension de la simulation en 3D (C++ et CUDA) avec intégration de la bibliothèque OpenVDB pour le traitement des géométries. Le rendu est fait par un compute shader GLSL exécutant un algorithme de ray marching volumétrique. Le shader évalue les normales par calcul de gradient sur la grille et modélise physiquement les interfaces eau/air (équations de Fresnel, réflexion, réfraction, absorption).

<table align="center" width="100%">
<tr>
<td align="center" width="50%">
<video src="https://github.com/user-attachments/assets/dbf55cb2-b622-4211-aec1-3ac2d258b711
" controls width="100%"></video>
<br><em>Visualisation 3D de la dynamique du fluide par nuage de points.</em>
</td>
<td align="center" width="50%">
<video src="https://github.com/user-attachments/assets/32d4fcb3-a1f2-4b3c-af54-099c1f9645d9" controls width="100%"></video>
<br><em>Rendu de l'eau via ray marching volumétrique. </em>
</td>
</tr>
</table>

## Reconstruction 3D par photogrammétrie
Reconstruction 3D d'objets réels par photogrammétie et synthèse d'images par rendu inverse.
<br>
**Technologies :** 
![RealityScan](https://img.shields.io/badge/RealityScan-%23000000.svg?style=flat&logo=epicgames&logoColor=white) ![Blender](https://img.shields.io/badge/Blender-%23F5792A.svg?style=flat&logo=blender&logoColor=white) ![Three.js](https://img.shields.io/badge/Three.js-black?style=flat&logo=three.dot.js&logoColor=white) ![Quarto](https://img.shields.io/badge/Quarto-%234169E1.svg?style=flat)
<br>
**[Consulter le projet complet et le visualiseur 3D interactif](https://harounjilani.github.io/Quarto/)**

<table align="center" width="50%">
<tr>
<td align="center" width="50%">
<img src="assets/3D_reconstructed_model.png" width="50%" alt="Reconstruction 3D" />
<br><em>Modèle 3D reconstruit et visualisé.</em>
</td>
</tr>
</table>

## ⚙️ Moteur de rendu temps réel (OpenGL)

Développement d'un moteur 3D en C++ et OpenGL reposant sur une architecture de rendu différé (deferred shading). Le pipeline graphique intègre la génération de G-Buffers via Multiple Render Targets (MRT) et l'application d'effets de post-traitement en espace écran.

**Fonctionnalités implémentées :**
*   **Shadow mapping :** calcul d'ombres portées directionnelles avec application d'un biais adaptatif et d'un filtrage PCF pour adoucir les contours.

*   **Bloom :** extraction des hautes lumières via un seuillage progressif pour éviter les artefacts, suivie d'un filtrage séparable pour diffuser l'effet lumineux.
*   **Post-processing :** application d'un algorithme de tone mapping et d'une correction gamma pour la conversion de l'image HDR en espace sRGB.


**Technologies :** 
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=flat&logo=c%2B%2B&logoColor=white) ![OpenGL](https://img.shields.io/badge/OpenGL-%23FFFFFF.svg?style=flat&logo=opengl) ![GLSL](https://img.shields.io/badge/GLSL-%23333333.svg?style=flat)

<table align="center" width="100%">
  <tr>
    <td align="center" width="50%">
      <img src="assets/shadows_only.png" width="100%" alt="Shadow mapping uniquement" />
      <br><em>Shadow mapping uniquement.</em>
    </td>
    <td align="center" width="50%">
      <img src="assets/bloom_only.png" width="100%" alt="Bloom uniquement" />
      <br><em>Bloom uniquement.</em>
    </td>
  </tr>
  <tr>
    <td align="center" colspan="2">
      <br>
      <img src="assets/final_result_1.png" width="80%" alt="Rendu final complet" />
      <br><em>Shadow mapping + bloom + tone mapping + correction gamma.</em>
    </td>
  </tr>
</table>

## 💡 Moteur de ray tracing
Développement d'un moteur de ray tracing en C++, étendu par la suite en un path tracer pour la simulation de l'illumination globale.

**Fonctionnalités implémentées :**
*   **Ray Tracing :** lancer de rayons classique gérant les ombres portées, ainsi que les matériaux transparents et miroirs.
*   **Path Tracing :** calcul de l'illumination globale basé sur la méthode de Monte-Carlo.
*   **Matériaux PBR :** gestion de la couleur, rugosité et métallicité avec le modèle de micro-facettes (Cook-Torrance/GGX).
*   **Structure d'accélération :** optimisation des performances via une structure de données BVH accélérée par l'heuristique SAH.
*   **Surfaces implicites :** Implémentation de l'algorithme de sphere tracing pour le rendu de géométries implicites.

**Technologies :** 
![C++](https://img.shields.io/badge/c++-%2300599C.svg?style=flat&logo=c%2B%2B&logoColor=white)

<table align="center" width="100%">
  <tr>
    <td align="center" width="33.33%">
      <img src="assets/conference.jpg" width="100%" alt="Scène Conference" />
      <br><em>Scène Conference (maillage).</em>
    </td>
    <td align="center" width="33.33%">
      <img src="assets/refraction_reflexion.jpg" width="100%" alt="Matériaux" />
      <br><em>Matériaux transparents et miroirs.</em>
    </td>
    <td align="center" width="33.33%">
      <img src="assets/sphere_tracing.jpg" width="100%" alt="Sphere Tracing" />
      <br><em>Rendu par sphere tracing (surfaces implicites).</em>
    </td>
  </tr>
  <tr>
    <td align="center" colspan="3">
      <br>
      <img src="assets/1024_spp_sponza_pbr.jpg" width="100%" alt="Rendu Path Tracing Sponza" />
      <br><em>Rendu final de la scène Sponza (textures PBR) par path tracing (1024 spp, 8 rebonds).</em>
    </td>
  </tr>
</table>
<br>


## Super Résolution d'Images

Développement d'un modèle d'apprentissage profond pour la super-résolution d'images. L'objectif est de reconstruire des images faciales haute définition (128x128) à partir d'entrées basse résolution (32x32).

**Technologies :** 
![Python](https://img.shields.io/badge/Python-%2314354C.svg?style=flat&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=flat&logo=TensorFlow&logoColor=white)

<table align="center" width="100%">
  <tr>
    <td align="center">
      <img src="assets/super_resolution.png" width="100%" alt="Comparaison des méthodes d'upscaling" />
      <br><em><b>De haut en bas :</b> 1. Entrée (32x32) | 2. Nearest neighbor | 3. Bicubique | 4. Super résolution (modèle) | 5. Réel (128x128)</em>
    </td>
  </tr>
</table>
<br>

## 🐜 Suivi Vidéo et analyse de colonies de fourmis

Création d'un logiciel d'analyse vidéo pour détecter et suivre les déplacements de fourmis à l'aide de la vision par ordinateur. Le programme calcule leur vitesse, repère les dépôts de phéromones et exporte toutes ces informations au format CSV. L'objectif final est d'utiliser ces données pour entraîner des intelligences artificielles capables de simuler le comportement d'une colonie.

**Technologies :** 
![Python](https://img.shields.io/badge/Python-%2314354C.svg?style=flat&logo=python&logoColor=white) ![OpenCV](https://img.shields.io/badge/OpenCV-%235C3EE8.svg?style=flat&logo=opencv&logoColor=white)

<div align="center">
  <a href="demo_fourmis">
    <video src="https://github.com/user-attachments/assets/cfaf3aad-8a0b-4b00-8ec3-9472d5414721" width="80%" alt="Démo vidéo du suivi de fourmis" />
  </a>
  <br><em>Démonstration du logiciel.</em>
</div>
<br>






