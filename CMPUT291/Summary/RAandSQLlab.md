# Relational Algebra and SQL Expressions

- product(maker,model,type) 

- pc(model,speed,ram,HD,price) 

- laptop(model,speed,ram,HD,price) 

- printer(model,color,type,price)

1. List the ***model*** for PCs that are faster than 150 MHz ?

   Relational Algebra :  

   $\pi_{model}(\sigma_{speed>150}(pc))$

   SQL : 

   `SELECT model FROM PC WHERE SPEED > 150`

   

2. List prices & models of all pc,laptop,printers.

   Relational Algebra (union compatibility) : 

   $\pi_{prices,models}(pc) \thinspace \cup \thinspace \pi_{prices,models}(laptop) \thinspace \cup \thinspace \pi_{prices,models}(printer) $

   SQL :

   `(SELECT prices, models FROM pc) UNION (SELECT prices, models FROM laptop) UNION (SELECT prices, models FROM printer)`

   

3. List makers that make laptops but not PCs.

   Relational Algebra (Multiple ways) :

   $\pi_{maker,model}(product)/\pi_{model}(laptop)$

   SQL (Multiple ways) :

   `SELECT maker FROM product WHERE type = 'laptop' EXCEPT SELECT maker FROM product WHERE type = 'PC'`

   

4. Which speeds are common in PCs and laptops?

   It's convenience to think two tables are two sets and how to apply set operation to obtain the desire result

   RA (Multiple ways) :

   $\pi_{speed}(pc) \thinspace \cap \thinspace \pi_{speed} (laptop)$

   or 

   $\sigma_{s1=s2}(\rho_{s1}\pi_{speed}(pc) \cross \rho_{s2}\pi_{speed}(laptop))$

   SQL (Multiple ways) :

   `(SELECT speed FROM pc) INTERSECT (SELECT speed FROM laptop)`

    

5. List makers and prices for makers that  produce pc.

   RA :

   $\pi_{makers,prices}(product\bowtie pc)$

   SQL :

   `SELECT maker, price FROM product, pc WHERE product.model IN (SELECT model FROM pc)`
   
   

6. List makers that make at least 2 different models

   RA :

   $\pi_{maker}(\sigma_{model<>model2}(product\bowtie product[maker,model2,type2]))$

   SQL :

   `SELECT DISTINCT p1.maker FROM product p1, product p2 WHERE p1.maker = p2.maker and p1.model <> p2.model`



7. Find all laptop models that are more expensive than the most expensive PC.

   RA :

   $\pi_{model}\sigma_{price>price2}(\pi_{model,price}(laptop) \thinspace \cross \thinspace \rho_{model2,price2}\pi_{model,price}(pc))$

   SQL :

   `SELECT laptop.model FROM laptop WHERE laptop.price > (SELECT MAX(PC.price) FROM PC)`

8.  Find the CPU speed and HD size for all PCs and  laptops with no duplicate rows in the output.

   `SELECT DISTINCT speed, HD FROM (SELECT * FROM pc UNION SELECT * FROM laptop)`

   `SELECT laptop.speed, laptop.HD FROM laptop UNION SELECT pc.speed, pc.hd FROM pc `



9. Find the makers, model and price of the  highest priced laptop.

```sqlite
SELECT p.maker, l1.model, l1.price FROM (product p JOIN laptop l1 ON p.model = l1.model) WHERE l1.price = (SELECT MAX(l2.price) FROM laptop l2);
```

- `join` : https://www.sqlite.org/optoverview.html#joins



10. 

