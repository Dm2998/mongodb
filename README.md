# mongodb
Labs-mongodb


#Mongodb Labs 

<br>
db.inventory.insertOne({ "_id": 10, "type": "electronic", "item": "ipad", "qty": 15, "price": 550 })
<br>
db.inventory.insertOne({ "_id": 11, "type": "electronic", "item": "iphone", "qty": 13, "price": 400 })
<br>
db.inventory.insertOne({ "_id": 12, "type": "consumables", "item": "print cartridge", "qty": 5 })#
<br>
db.inventory.insertOne({ "_id": 14, "type": "electronic", "item": "imac", "qty": 10, "price": 400 })
<br>
db.inventory.insertOne({ "_id": 15, "type": "book", "item": "yes to noSQL", "qty": 10, "price": 40 })
<br>
db.inventory.insertOne({ "_id": 16, "type": "book", "item": "Mongo Mongo", "qty": 10, "price": 40 })
<br>
db.employee.insertOne({ "firstname": "Peter", "lastName": "Smith" })
<br>
db.order.insertOne({
  "_id": 99999,
  "name": { "first": "John", "last": "McCarthy" },
  "orderDate": new Date("Sep 04, 2013"),
  "ShippingAddress": { "line1": "Belgard Road", "line2": "Tallaght", "city": "Dublin" },
  "lineItems": [
    { "product": "screws", "qty": 10, "uom": "kg", "unitPrice": 10.00 },
    { "product": "fuel", "qty": 30, "uom": "litres", "unitPrice": 3.00 },
    { "product": "tiles", "qty": 2, "uom": "pallots", "unitPrice": 259.00, "colour": "cream" }
  ]
});
<br>




db.order.insertOne({  "_id": 99999,  "name": { "first": "John", "last": "McCarthy" },  "orderDate": new Date("Sep 04, 2013"),  "ShippingAddress": { "line1": "Belgard Road", "line2":"Tallaght", "city": "Dublin" },  "lineItems": [    { "product": "screws", "qty": 10, "uom": "kg", "unitPrice": 10.00 },    { "product": "fuel", "qty": 30, "uom": "litres","unitPrice": 3.00 },    { "product": "tiles", "qty": 2, "uom": "pallots", "unitPrice": 259.00, "colour": "cream" }  ]})
------------------------------------------------

<br>

db.inventory.update(
   { "type": "book", item: "journal", "price": 10 },
   { $set: { "qty": 10 } },
   { "upsert": true }
);

<br>
db.inventory.update(
   { "type": "book", "item": "journal", "price": 10 },
   { $set: { "qty": 999 } },
   { "upsert": true }
);

<br>
db.inventory.update(
   { "type": "book" },
   { $inc: { "qty": 5 } }
);

<br>
db.inventory.update(
   { "type": "book" },
   { $inc: { "qty": 5 } },
   { "multi": true }
);

<br>

db.inventory.find()


<br>


db.inventory.find({ "type": "book", "item": "journal", "price": { $gt: 5 }}).pretty();


<br>




db.inventory.find({ $or: [{"qty": { $gt: 100 } },{ "price": { $lt: 450 } }]} ) .pretty() 

<br>

-- equivalent to the SQL OR and AND clause

db.inventory.find( { "type": "book", $or: [ { "qty": { $gt: 10 } }, { "price": { $lt: 450 } } ]} ).pretty() 


<br>


db.order.find( { "name.first":"John" }).pretty() 



<br>

#Exce
<br>
Step 2: Repeat the MongoDB command to find inventory documents that are either electronic or book and have a price less than 200.
<br>

db.inventory.find({$or: [{ "type": "electronic" },{ "type": "book" }],"price": { $lt: 200 }}).pretty();

<br>

Step 2: Repeat the MongoDB command to find inventory documents that are of type book, with an item name journal, and have a price greater than 5.
db.inventory.find({"type": "book","item": "journal","price": { $gt: 5 }}).pretty();

<br>


Step 2: Repeat the MongoDB command to find all documents that have a price in the range of 101 to 699.
<br>
db.inventory.find({ $and: [{ "price": { $gte: 101 } },{ "price": { $lte: 699 } }]}).pretty();

<br>


4.	Find an order that has a firstname of John and last name of Smith whose shipping address is in Dublin.
<br>

db.order.find({"name.first": "John","name.last": "Smith","shipping.address": "Dublin"}).pretty();

<br>

Delete inventory documents that are type book or electronic.

<br>

db.inventory.remove({$or: [{ "type": "book" },{ "type": "electronic" }]});

<br>
