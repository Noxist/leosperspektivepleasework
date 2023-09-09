+++
title = "test für zufällige adresse"
date = "2023-09-09"
draft = false
pinned = false
+++
```
<!DOCTYPE html>
<html>
<head>
	<title>Zufällige Adresse</title>
</head>
<body>
	<h1>Zufällige Adresse</h1>
	<p>Name: <span id="name"></span></p>
	<p>Nachname: <span id="surname"></span></p>
	<p>E-Mail-Adresse: <span id="email"></span></p>
	<p>Adresse: <span id="address"></span></p>

	<script src="https://cdnjs.cloudflare.com/ajax/libs/Faker/3.1.0/faker.min.js"></script>
	<script>
		var name = faker.name.firstName();
		var surname = faker.name.lastName();
		var email = faker.internet.email();
		var street = faker.address.streetAddress();
		var city = faker.address.city();
		var zipCode = faker.address.zipCode();

		var address = street + "\n" + zipCode + " " + city;

		document.getElementById("name").innerHTML = name;
		document.getElementById("surname").innerHTML = surname;
		document.getElementById("email").innerHTML = email;
		document.getElementById("address").innerHTML = address;
	</script>
</body>
</html>
```