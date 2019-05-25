# Users

## DataType

```
colset User = product Id*Username*Password*UserType*UserDetails;
colset UserDetails = product Name*Surname*DeliveryAdress;
```

## Test Data

```
val adminType = 0;
val clientType = 1;
val adminId = GenerateId();
val clientId = GenerateId();
val clientDetails = ("Alex","Buzdugan","Strada Bucuresti");
val client = (clientId,"Username","password",clientType,clientDetails);
val adminDetails = ("Admin","Admin","Strada Bucuresti 2");
val admin = (adminId,"Admin","password",adminType,adminDetails);
val users = [client,admin];
```

## Functions

```
fun IsAdmin((_,_,_,userType,_)) = userType = 0;
fun IsRegistered(users, user) = contains users [user];
fun CanLogin(users, user) = contains users [user];
fun RegisterUser(users, user) = ins users user;
```

## Tests

```
IsAdmin(client);
IsAdmin(admin);
IsRegistered(users,client);
IsRegistered(users,admin);
CanLogin(users,client);
CanLogin(users,admin);
```