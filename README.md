# README - Workshop Dev 3 : VSCode et Foundry  

Ce guide explique comment installer et utiliser Visual Studio Code (VSCode) et Foundry pour créer, tester et déployer des contrats intelligents Ethereum.  

## Prérequis  
- Un ordinateur avec un système d'exploitation compatible (Windows, macOS ou Linux).  
- Une connexion internet pour les téléchargements.  

---

## Étape 1 : Installer Visual Studio Code  
Téléchargez et installez Visual Studio Code à partir du lien suivant :  
[Visual Studio Code - Download](https://code.visualstudio.com/Download)  

---

## Étape 2 : Installer WSL (Windows uniquement)  

![image](https://github.com/user-attachments/assets/6966fd21-0787-4473-a9a5-83d78bc01a8b)  

Pour les utilisateurs de Windows, installez le **Windows Subsystem for Linux (WSL)** :  
- Ouvrez un terminal PowerShell en tant qu'administrateur et exécutez la commande :  
  ```bash  
  wsl --install  
  ```  
- [Guide d'installation WSL](https://learn.microsoft.com/en-us/windows/wsl/install)  

---

## Étape 3 : Installer Foundry  
1. Ouvrez votre terminal et accédez à WSL :  
   ```bash  
   wsl  
   ```  
2. Exécutez la commande suivante pour installer Foundry :  
   ```bash  
   curl -L https://foundry.paradigm.xyz | bash  
   ```  
3. Suivez les instructions pour configurer Foundry.  

---

## Étape 4 : Initialiser un projet Foundry  
1. Déplacez-vous vers votre dossier de travail, par exemple `KS_DEV`.  
2. Créez un dossier pour votre projet Foundry :  
   ```bash  
   mkdir smart_contracts  
   cd smart_contracts  
   forge init hello_foundry  
   ```  
3. Ouvrez ce dossier dans VSCode :  
   ```bash  
   cd hello_foundry  
   code .  
   ```  
4. Ouvrez le terminal intégré dans VSCode avec **Ctrl + J** et lancez WSL :  
   ```bash  
   wsl  
   ```  
5. Construisez le projet pour vérifier qu'il fonctionne :  
   ```bash  
   forge build  
   ```  
6. Exécutez les tests pour valider le projet :  
   ```bash  
   forge test  
   ```  
7. Explorez le fichier `Counter.sol` dans le dossier `src`.  

---

## Étape 5 : Déployer le contrat  
1. Créez un fichier `.env` à la racine du projet et ajoutez-y les informations suivantes :  
   ```env  
   PRIVATE_KEY=<PRIVATE_KEY>  
   INFURA_API_KEY=<INFURA_API_KEY>  
   ```
   
![image](https://github.com/user-attachments/assets/260ea4ed-4855-4892-abbe-eb9b70bbd3b8)  

   - **PRIVATE_KEY** : Votre clé privée Metamask (uniquement pour un wallet de développement).  
   - **INFURA_API_KEY** : Obtenez cette clé en créant un compte sur [Infura](https://www.infura.io/) et en générant une API Key.  
2. Vérifiez que votre wallet contient des **ETH Sepolia** pour payer les frais de gaz.  
3. Déployez le contrat avec la commande suivante :  
   ```bash  
   forge create --rpc-url https://sepolia.infura.io/v3/<INFURA_API_KEY> --private-key <PRIVATE_KEY> src/Counter.sol:Counter  
   ```  
4. Copiez l'adresse du contrat et vérifiez son déploiement sur [Sepolia Etherscan](https://sepolia.etherscan.io).  

---

## Étape 6 : Vérifier le contrat  
1. Exécutez la commande suivante pour interagir avec votre contrat :  
   ```bash  
   forge script script/Counter.s.sol:CounterScript --rpc-url https://sepolia.infura.io/v3/<INFURA_API_KEY> --broadcast --verify  
   ```  
2. Vous pouvez maintenant interagir avec votre contrat directement depuis **Etherscan**.  

---  

## Étape 7 : Créez un repo GitHub  
1. Initialisez un dépôt Git dans votre projet :
   ```bash  
   git status
   ```
2. Si pas de repo déjà créé, faites git init, sinon, faites directement git add .
   ```bash  
   git init  
   git add .  
   git commit -m "Initial commit with Foundry project"  
   ```  
3. Créez un nouveau dépôt sur GitHub.  
4. Liez votre projet local à GitHub :  
   ```bash  
   git remote add origin <URL_DU_DEPOT_GITHUB>  
   git branch -M main  
   git push -u origin main  
   ```  
5. Ajoutez les fonctions importantes (build, test, déploiement, etc.) dans le dépôt pour que les autres puissent les utiliser.  

👉 Retrouvez les détails de git ici : [Workshop Dev 2: Git & Github](https://docs.google.com/presentation/d/1ehAre6UtXctiomXbZBmi_3krjUoMDWMUtSoQ7RvZLUk/edit?usp=sharing).  

---  

## Ressources utiles  
- [Documentation Foundry](https://book.getfoundry.sh/)  
- [Sepolia Etherscan](https://sepolia.etherscan.io)  
- [Guide WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
- [Workshop Dev 2: Git & Github](https://docs.google.com/presentation/d/1ehAre6UtXctiomXbZBmi_3krjUoMDWMUtSoQ7RvZLUk/edit?usp=sharing).  
