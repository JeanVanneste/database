# Compléments de bases de données

## Requêtes simples
1. Prix maxima, minima, prix moyens, nombres de vendeurs par espèces

```sql
SELECT arbres.espece , max(prix), min(prix), avg(prix), count(vendeur) 
FROM stock INNER JOIN arbres ON arbres.id = stock.espece 
GROUP BY arbres.espece;
```
2. Vendeurs de pins par code postal
```sql
SELECT nom, prenom, codePostal 
FROM arbres INNER JOIN stock ON arbres.id = stock.espece
    INNER JOIN vendeur ON stock.vendeur = vendeur.id
    INNER JOIN adresse ON vendeur.adresse = adresse.id 
WHERE arbres.espece = 'Pin' 
ORDER BY codePostal;
```
3. Totaux de stocks par vendeurs
```sql
SELECT nom, prenom, SUM(stock) 
FROM vendeur INNER JOIN stock ON vendeur.id = stock.vendeur
GROUP BY vendeur.id
ORDER BY vendeur.nom;
``` 
4. Vue d'ensemble de toute la DB sous forme de VUE
```sql
CREATE VIEW db AS 
SELECT arbres.espece, vendeur.nom, vendeur.prenom, adresse.rue, adresse.numero,  ville.codePostal, ville.nom as ville, pays.code, pays.nom as pays, stock.prix, stock.stock
FROM arbres JOIN stock ON arbres.id = stock.espece
JOIN vendeur ON vendeur.id = stock.vendeur
JOIN adresse ON vendeur.adresse = adresse.id
JOIN ville ON ville.codePostal = adresse.codePostal
JOIN pays ON adresse.codePays = pays.code
ORDER BY arbres.espece, stock.prix; 
```
5. Requête pour augmenter de 10% le prix de vente de tous les pins

6. Requête pour afficher tous les prix (HTVA) et les les prix (TVAC) pour les chênes de tout les vendeurs

7. Requête permettant d'extraire les informations nécessaires pour créer des étiquettes d'adresses pour tout les vendeurs de 7531 Tournai