# Users

## DataType

```
// DeliveryType
// 0 - NotSet
// 1 - Pay at delivery
// 2 - Pay online

// OrderStatus
// 0 - Started
// 1 - InProgress -- not delivered
// 2 - Finished -- delivered
// 3 - Rejected 

colset Order = product Id*UserId*Products*Status*DeliveryType*Total;
```

## Test Data

```
val client1Type = 1;
val client2Type = 1;
val client1Id = GenerateId();
val client2Id = GenerateId();
val client1Details = ("client1","client1","Strada Bucuresti");
val client2Details = ("client2","client2","Strada Bucuresti 2");
val client1 = (client1Id,"Username","password",client1Type,client1Details);
val client2 = (client2Id,"client2","password",client2Type,client2Details);
val users = [client1,client2];

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

val client1OrderId = GenerateId();
val client1OrderDeliveryType = 0
val client1OrderStatus = 0;
val client1Order = (client1OrderId, client1Id, [bread,cheese], client1OrderStatus, client1OrderDeliveryType,0)

val client2OrderId = GenerateId();
val client2OrderDeliveryType = 0;
val client2OrderStatus = 0;
val client2Order = (client2OrderId, client2Id, [sausage], client2OrderStatus, client2OrderDeliveryType,0)

val orders = [client1Order, client2Order];
```

## Functions

```
fun GetUserOrders((userId,_,_,_,_), orders) = List.filter (fn((_,id,_,_,_,_)) => id=userId) orders;

fun GetOrder(orderId, orders)= List.nth(List.filter (fn((id,_,_,_,_,_)) => id=orderId) orders,0);

fun AddProductInUserOrder((id,userId,products,status,deliveryType,total),product,quantity) = (id,userId,ins products product,status,deliveryType,total);

fun SetOrderDeliveryType((id,userId,products,status,deliveryType,total), orderDeliveryType) = (id,userId,products,status,orderDeliveryType,total);

fun SetOrderStatus((id,userId,products,status,deliveryType,total), orderStatus) = (id,userId,products,orderStatus,deliveryType,total);

fun CalculateOrderTotal((id,userId,products,status,deliveryType,total)) = (id,userId,products,status,deliveryType,GetProductsTotalValue(products));

fun CreateUserOrder((client1Id,_,_,_,_)) = (GenerateId(), client1Id, []:(int*string*string*int*int) list, 0, 0,0);

fun AddUserOrderToList(order,orders) = ins orders order;

fun GetFinishedOrders(orders) = List.filter (fn((_,_,_,status,_,_)) => status = 2) orders;

fun GetOrdersTotalValue[] = 0
  | GetOrdersTotalValue((_,_,products,_,_,_)::orders) = GetProductsTotalValue(products) + GetOrdersTotalValue orders;
```

## Tests

```
GetUserOrders(client1, orders);
GetUserOrders(client2, orders);
GetOrder(client1OrderId,orders);
AddProductInUserOrder(client1Order,bread,1);
SetOrderDeliveryType(client1Order,1);
SetOrderStatus(client1Order,1);
CalculateOrderTotal(client1Order);
CreateUserOrder(client1);

//Full integration
val newOrder = CreateUserOrder(client1);
GetUserOrders(client1, orders);
SetOrderDeliveryType(newOrder,1);
SetOrderStatus(newOrder,1);
val test = AddProductInUserOrder(newOrder,bread,1);
val test = AddProductInUserOrder(test,bread,1);
CalculateOrderTotal(test);
GetOrdersTotalValue(GetFinishedOrders(orders));
```