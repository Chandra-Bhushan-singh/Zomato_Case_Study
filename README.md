# Zomato_Case_Study

Dataset : https://docs.google.com/spreadsheets/d/1JgNHxTixDA50W1l6pNFmHKRaX1a9QnXrpGLsJtzo6Gg/edit?usp=share_link

1.	Select a particular Database.


             Use Zomato           

2.	Count number of rows.


           Select count(*) from orders
![image](https://user-images.githubusercontent.com/131191068/236327560-6ae3f1bf-56ef-4edf-a604-254e56815b88.png)

 

3.	return a random records.
 
        SELECT * FROM users
        ORDER BY rand() LIMIT 5
    
    
    ![image](https://user-images.githubusercontent.com/131191068/236327664-78bdeab4-6d46-4964-9ec8-66f66a916732.png)


4.	Find null values.

         SELECT * FROM orders
         WHERE restaurant_rating IS NULL;
      

![image](https://user-images.githubusercontent.com/131191068/236328328-b9117dd3-dc69-4bf3-81eb-4178f2aba726.png)

 

5.	Find the number of order placed by each customer.



        SELECT t2.name, count(*) as '#orders' from orders t1
        JOIN users t2
        ON t1.user_id = t2.user_id
        GROUP BY t2.user_id
 
 ![image](https://user-images.githubusercontent.com/131191068/236328387-4bcce10a-3e18-49e0-930f-b55170d5606b.png)

 
6.	Find restaurant with most number of menu items.


              SELECT r_name, Count(*) as 'menu_items' FROM restaurants t1
              JOIN menu t2 
              ON t1.r_id = t2.r_id
              GROUP BY t2.r_id

![image](https://user-images.githubusercontent.com/131191068/236328521-3d900fed-42c0-4e10-aa09-80878d066833.png)


7.	Find number votes and average rating for all the restaurants.

             SELECT r_name,count(*) as 'num_votes', ROUND(AVG(restaurant_rating),2) as 'rating'
             FROM orders t1
             JOIN restaurants t2
             ON t1.r_id = t2.r_id
             WHERE restaurant_rating IS NOT NULL
             GROUP BY t1.r_id;
             
![image](https://user-images.githubusercontent.com/131191068/236330928-2a862f7d-7901-4aa4-a29f-ab4912aae699.png)

 

8.	Find the food that is being sold at most number of restaurant.

              SELECT f_name,Count(*) FROM menu t1
              JOIN food t2
              ON t1.f_id = t2.f_id
              GROUP BY t1.f_id
              ORDER BY Count(*) DESC LIMIT 1;
              
 ![image](https://user-images.githubusercontent.com/131191068/236331240-2a9a7c47-bae8-4672-9d73-4fcd09dcf7be.png)


9.	Find restaurant with max revenue in a given month.

              SELECT r_name,SUM(amount) AS 'revenue' FROM orders t1
              JOIN restaurants t2
              ON t1.r_id = t2.r_id
              WHERE MONTHNAME(DATE(date)) = 'May'
              GROUP BY t1.r_id
              ORDER BY revenue DESC LIMIT 1;

10.	 Find restaurant with sales > x

               SELECT r_name,SUM(amount) as 'revenue' FROM orders t1
               JOIN restaurants t2
               ON t1.r_id = t2.r_id
               GROUP BY t1.r_id
               HAVING revenue > 1500;
![image](https://user-images.githubusercontent.com/131191068/236331659-6d65a7e5-f615-4761-a30e-99344ecb9171.png)

 

11.	find customers who have never ordered.

              SELECT user_id,name FROM users
              EXCEPT
              SELECT t1.user_id,name FROM orders t1
              JOIN users t2
              ON t1.user_id = t2.user_id;
  ![image](https://user-images.githubusercontent.com/131191068/236332209-05fdcb39-3eb4-4f47-99a8-8aef5085df72.png)
            

12.	Show order details of a particular customer in a given data range.

              SELECT t1.order_id,f_name,date FROM orders t1
              JOIN order_details t2
              ON t1.order_id = t2.order_id
              JOIN food t3
              ON t2.f_id = t3.f_id
              WHERE user_id = 2  AND date BETWEEN '2022-05-15' AND '2022-07-15';



13.	customer favorite food

                SELECT t1.user_id,t3.f_id, name, count(*) FROM users t1
                JOIN orders t2
                ON t1.user_id = t2.user_id
                JOIN order_details t3
                ON t2.order_id = t3.order_id
                GROUP BY t1.user_id, t3.f_id
                ORDER BY count(*) DESC;
              
 ![image](https://user-images.githubusercontent.com/131191068/236332332-214cce73-dc49-4a44-bb9a-0ef3ec84f3b3.png)


14.	find most costly restaurant (Avg price/dish).

              SELECT r_name,SUM(price)/COUNT(*) AS 'Avg_price' FROM menu t1
              JOIN restaurants t2
              ON t1.r_id = t2.r_id
              GROUP BY t1.r_id
              ORDER BY Avg_price ASC LIMIT 1;
 ![image](https://user-images.githubusercontent.com/131191068/236332528-169c2e30-b969-4f0d-a740-469eaa16c34e.png)


15.	find delivery partner compensation using the formula (#deveveries * 100 + 1000*avg_rating)

             SELECT partner_name,COUNT(*) * 100  + AVG(delivery_rating)*1000 AS 'salary'
             FROM orders t1
             JOIN delivery_partner t2
             ON t1.partner_id = t2.partner_id
             GROUP BY t1.partner_id
             ORDER BY salary DESC;
 ![image](https://user-images.githubusercontent.com/131191068/236332580-515ae512-93f9-481c-af84-05e8897fd4c7.png)


19. find all the veg restaurants.

             SELECT * FROM menu t1
             JOIN food t2 
             ON t1.f_id = t2.f_id
             JOIN restaurants t3 
             ON t1.r_id = t3.r_id
             GROUP BY t1.r_id
             HAVING MIN(type) = 'Veg' AND MAX(type) = 'Veg';
![image](https://user-images.githubusercontent.com/131191068/236332682-2a83af4f-77fb-4dcd-aa53-36ae54e7fac8.png)
 

20. Find min and max order value for all the customers

             SELECT name,MIN(amount),MAX(amount),AVG(amount) FROM orders t1
             JOIN users t2
             ON t1.user_id = t2.user_id
             GROUP BY t1.user_id;
![image](https://user-images.githubusercontent.com/131191068/236332798-bd275537-20f2-4c02-a680-087b8ab71716.png)

 
