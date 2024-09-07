# La-gestion-des-utilisateurs-sur-Windows
La gestion des utilisateurs sur Windows peut se faire de plusieurs manières, que ce soit via l'interface graphique (GUI) ou par des commandes en ligne de commande (CLI). Voici un aperçu des principales méthodes pour gérer les utilisateurs sur Windows.

### 1. **Gestion des utilisateurs via l'interface graphique**

#### a. **Panneau de configuration**
   - **Accès :** `Panneau de configuration > Comptes d'utilisateurs > Gérer les comptes d'utilisateurs`
   - Cette méthode permet d'ajouter, de supprimer, ou de modifier des comptes utilisateurs, ainsi que de changer les mots de passe et d'ajuster les niveaux de privilèges (administrateur ou utilisateur standard).

#### b. **Paramètres de Windows 10/11**
   - **Accès :** `Paramètres > Comptes > Famille et autres utilisateurs`
   - Cette interface permet d'ajouter des comptes Microsoft, des comptes locaux, des comptes professionnels ou scolaires, ainsi que de gérer les utilisateurs familiaux.

#### c. **Gestion des utilisateurs et des groupes locaux (Local Users and Groups)**
   - **Accès :** `Gestion de l'ordinateur > Utilisateurs et groupes locaux`
   - Cette console est plus avancée et permet de créer, modifier, et supprimer des comptes utilisateurs et groupes, de définir des stratégies de mot de passe, et de gérer les membres des groupes.

### 2. **Gestion des utilisateurs via la ligne de commande**

#### a. **Commande `net user`**
   - **Ajouter un utilisateur :**
     ```cmd
     net user nom_utilisateur mot_de_passe /add
     ```
   - **Supprimer un utilisateur :**
     ```cmd
     net user nom_utilisateur /delete
     ```
   - **Modifier un mot de passe utilisateur :**
     ```cmd
     net user nom_utilisateur nouveau_mot_de_passe
     ```
   - **Liste des utilisateurs :**
     ```cmd
     net user
     ```
   - **Ajouter un utilisateur au groupe des administrateurs :**
     ```cmd
     net localgroup Administrateurs nom_utilisateur /add
     ```

#### b. **Commande `wmic useraccount`**
   - **Liste des utilisateurs :**
     ```cmd
     wmic useraccount get name
     ```
   - **Vérifier l'état d'un compte utilisateur (activé ou désactivé) :**
     ```cmd
     wmic useraccount where name="nom_utilisateur" get name,disabled
     ```

#### c. **Commande `PowerShell`**
   - **Créer un utilisateur local :**
     ```powershell
     New-LocalUser -Name "nom_utilisateur" -Password (ConvertTo-SecureString "mot_de_passe" -AsPlainText -Force) -FullName "Nom complet"
     ```
   - **Supprimer un utilisateur local :**
     ```powershell
     Remove-LocalUser -Name "nom_utilisateur"
     ```
   - **Ajouter un utilisateur au groupe des administrateurs :**
     ```powershell
     Add-LocalGroupMember -Group "Administrateurs" -Member "nom_utilisateur"
     ```
   - **Lister tous les utilisateurs locaux :**
     ```powershell
     Get-LocalUser
     ```

### 3. **Gestion des utilisateurs via l'Active Directory**

Dans les environnements professionnels utilisant un domaine Windows, la gestion des utilisateurs est souvent effectuée via Active Directory (AD). Voici les principales méthodes :

#### a. **Active Directory Users and Computers (ADUC)**
   - **Accès :** `Outils d'administration > Utilisateurs et ordinateurs Active Directory`
   - Cette interface permet de gérer les utilisateurs, les groupes, et les ordinateurs dans un domaine Active Directory. Vous pouvez créer des utilisateurs, attribuer des permissions, déplacer des utilisateurs entre des unités organisationnelles (OU), et bien plus encore.

#### b. **Commande `dsadd` (pour ajouter un utilisateur à Active Directory)**
   - **Ajouter un utilisateur :**
     ```cmd
     dsadd user "CN=Nom Utilisateur,OU=Utilisateurs,DC=nom_domaine,DC=com" -samid nom_utilisateur -pwd mot_de_passe -memberof "CN=Utilisateurs du domaine,CN=Users,DC=nom_domaine,DC=com"
     ```

#### c. **PowerShell pour Active Directory**
   - **Créer un utilisateur dans Active Directory :**
     ```powershell
     New-ADUser -Name "Nom Utilisateur" -GivenName "Prénom" -Surname "Nom" -SamAccountName "nom_utilisateur" -UserPrincipalName "nom_utilisateur@nom_domaine.com" -Path "OU=Utilisateurs,DC=nom_domaine,DC=com" -AccountPassword (ConvertTo-SecureString "mot_de_passe" -AsPlainText -Force) -Enabled $true
     ```
   - **Supprimer un utilisateur dans Active Directory :**
     ```powershell
     Remove-ADUser -Identity "nom_utilisateur"
     ```

### 4. **Gestion des groupes utilisateurs**

Windows permet également de gérer des groupes d'utilisateurs, ce qui facilite l'administration de grandes équipes.

#### a. **Ajouter un utilisateur à un groupe :**
   - Via ligne de commande :
     ```cmd
     net localgroup nom_groupe nom_utilisateur /add
     ```
   - Via PowerShell :
     ```powershell
     Add-LocalGroupMember -Group "nom_groupe" -Member "nom_utilisateur"
     ```

#### b. **Supprimer un utilisateur d'un groupe :**
   - Via ligne de commande :
     ```cmd
     net localgroup nom_groupe nom_utilisateur /delete
     ```
   - Via PowerShell :
     ```powershell
     Remove-LocalGroupMember -Group "nom_groupe" -Member "nom_utilisateur"
     ```

### Conclusion

La gestion des utilisateurs sur Windows peut être effectuée à différents niveaux en fonction des besoins de l'utilisateur ou de l'administrateur. Les outils graphiques sont pratiques pour des tâches simples et visuelles, tandis que les lignes de commande et PowerShell offrent une flexibilité et une automatisation accrues pour les tâches plus complexes ou répétitives. Active Directory ajoute une couche supplémentaire de gestion pour les environnements de réseau d'entreprise.
