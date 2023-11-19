# mongodb
Labs-mongodb


mongo

db.inventory.insertOne({ "_id": 10, "type": "electronic", "item": "ipad", "qty": 15, "price": 550 })
db.inventory.insertOne({ "_id": 11, "type": "electronic", "item": "iphone", "qty": 13, "price": 400 })
db.inventory.insertOne({ "_id": 12, "type": "consumables", "item": "print cartridge", "qty": 5 })
db.inventory.insertOne({ "_id": 14, "type": "electronic", "item": "imac", "qty": 10, "price": 400 })
db.inventory.insertOne({ "_id": 15, "type": "book", "item": "yes to noSQL", "qty": 10, "price": 40 })
db.inventory.insertOne({ "_id": 16, "type": "book", "item": "Mongo Mongo", "qty": 10, "price": 40 })

db.employee.insertOne({ "firstname": "Peter", "lastName": "Smith" })

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

---------------------------------------------


db.order.insertOne({  "_id": 99999,  "name": { "first": "John", "last": "McCarthy" },  "orderDate": new Date("Sep 04, 2013"),  "ShippingAddress": { "line1": "Belgard Road", "line2":"Tallaght", "city": "Dublin" },  "lineItems": [    { "product": "screws", "qty": 10, "uom": "kg", "unitPrice": 10.00 },    { "product": "fuel", "qty": 30, "uom": "litres","unitPrice": 3.00 },    { "product": "tiles", "qty": 2, "uom": "pallots", "unitPrice": 259.00, "colour": "cream" }  ]})
------------------------------------------------



db.inventory.update(
   { "type": "book", item: "journal", "price": 10 },
   { $set: { "qty": 10 } },
   { "upsert": true }
);

db.inventory.update(
   { "type": "book", "item": "journal", "price": 10 },
   { $set: { "qty": 999 } },
   { "upsert": true }
);

db.inventory.update(
   { "type": "book" },
   { $inc: { "qty": 5 } }
);

db.inventory.update(
   { "type": "book" },
   { $inc: { "qty": 5 } },
   { "multi": true }
);


//////////////////////////////////////////////////////
db.inventory.find()

/////////////////////////////



db.inventory.find({ "type": "book", "item": "journal", "price": { $gt: 5 }}).pretty();



/////////////////////////////////////////



db.inventory.find({ $or: [{"qty": { $gt: 100 } },{ "price": { $lt: 450 } }]} ) .pretty() 

///////////////////////////////////////

-- equivalent to the SQL OR and AND clause

db.inventory.find( { "type": "book", $or: [ { "qty": { $gt: 10 } }, { "price": { $lt: 450 } } ]} ).pretty() 



//////////////////////////////////


db.order.find( { "name.first":"John" }).pretty() 



//////////////////////////////////////////////

excessive
Step 2: Repeat the MongoDB command to find inventory documents that are either electronic or book and have a price less than 200.

db.inventory.find({$or: [{ "type": "electronic" },{ "type": "book" }],"price": { $lt: 200 }}).pretty();

//////////////////////////////////////

Step 2: Repeat the MongoDB command to find inventory documents that are of type book, with an item name journal, and have a price greater than 5.
db.inventory.find({"type": "book","item": "journal","price": { $gt: 5 }}).pretty();

/////////////////////////////////////////////


Step 2: Repeat the MongoDB command to find all documents that have a price in the range of 101 to 699.
db.inventory.find({ $and: [{ "price": { $gte: 101 } },{ "price": { $lte: 699 } }]}).pretty();




//////////////////////////////////////////

4.	Find an order that has a firstname of John and last name of Smith whose shipping address is in Dublin.
db.order.find({"name.first": "John","name.last": "Smith","shipping.address": "Dublin"}).pretty();

///////////////////////////////////////////////

Delete inventory documents that are type book or electronic.

db.inventory.remove({$or: [{ "type": "book" },{ "type": "electronic" }]});
