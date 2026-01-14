## Tables
```
  sellers
  - id
  - name
  - email

  user
  - id
  - name
  - email

  products
  - id
  - name
  - category
  - price

  product_seller_map
  - id
  - productid
  - sellerid

  categories
  - id
  - name

  order
  - id
  - userid
  - amount
  - payment
  - date

  orderitems
  - id
  - orderid
  - productid
  - sellerid
  - quantity

  payment
  - paymentMethod
  - status

  paymentMethod
  - id
  - name
```
## SQL Queries
```sql
-- for seller, total revenue last week
select o.sellerid, sum(p.price) from sellers s inner join (orderItems o inner join products p on o.productid == p.id) on s.id == p.seller_id 
where o.date > '2026-01-01'
group by s.id;

-- top 10 selling product by yearly revenue
-- we are filtering products sold last year, idk if its strictly top 10 products with yearly revenue
select p.name, sum(o.quantity * p.price) as revenue from products p inner join orderItems o on p.id == o.productid 
where o.date > '2025-01-01'
group by p.name order by revenue desc limit 10

-- for buyer, expense per category
select u.name, sum(p.price) from users u inner join (order o inner join orderitems oi on o.id = oi.orderid) inner join products p on p.id = oi.productid
group by p.category

-- top 10 product purchased for user 1
select p.name, sum(o.amount) from order o inner join orderItems oi on oi.orderid == o.id inner join products p on oi.productid = p.id
where o.userid = 1
order by sum(o.amount) desc
limit 10
```

### Notes

How to fast query
- Indexing
- Partitioning
- Sharing
  - 
