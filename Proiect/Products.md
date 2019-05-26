# Products

## DataType

```
colset Category = STRING;
colset Price = product INT*STRING;
colset Product = product Id*Description*Category*Price*Quantity;
```

## Test Data

```

val breadId = GenerateId();
val breadCategory = "Bakery";
val breadPrice = 10;
val breadDescription = "Bread"
val breadQuantity = 100;
val bread = (breadId,breadDescription,breadCategory,breadPrice,breadQuantity);

val cheeseId = GenerateId();
val cheeseCategory = "Dairy";
val cheesePrice = 20;
val cheeseDescription = "Cheese";
val cheeseQuantity = 50;
val cheese = (cheeseId,cheeseDescription,cheeseCategory,cheesePrice,cheeseQuantity);

val sausageId = GenerateId();
val sausageCategory = "Meat";
val sausagePrice = 30;
val sausageDescription = "Sausage";
val sausageQuantity = 30;
val sausage = (sausageId,sausageDescription,sausageCategory,sausagePrice,sausageQuantity);

val products = [bread,sausage,cheese];
```

## Functions

```
fun GetProducts(productList) = productList;
fun GetQuantityForProduct(products, productId) = rmall 0 (map (fn (id,_,_,_,quantity) => if (id=productId) then quantity else 0) products)
fun FilterProducts (products, category) =  List.filter (fn((_,_,c,_,_)) => c=category) products;
fun SetProductQuantity (productId, quantity, []) = []
    | SetProductQuantity (productId, quantity, (id,a,b,c,q) :: products) = (if id = productId then (id,a,b,c,quantity) else (id,a,b,c,q)) :: (SetProductQuantity (productId,quantity, products));
fun GetProduct (products, productId) = List.nth(List.filter (fn((id,_,_,_,_)) => id=productId) products, 0);
fun RemoveProduct(products, productId) = rmall (GetProduct(products, breadId)) products;
```

## Tests

```
GetProducts(products);
FilterProducts(products,"Bakery");
FilterProducts(products,"Meat");
FilterProducts(products,"Dairy");
FilterProducts(products,"None");
GetQuantityForProduct(products, breadId);
GetQuantityForProduct(SetProductQuantity(breadId, 300,products), breadId);
GetProduct(products,breadId);
RemoveProduct(products,breadId);
```