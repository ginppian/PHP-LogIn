Comprobar Usuario y Contraseña
============

```
<?php

$myPass = '1234';
$myCorreo = 'adantkm@gmail.com';

// Conectamos
$pdo = new PDO(
    'mysql:host=127.0.0.1;dbname=paracrecer',
    'root',
    '',
    array(PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8")
);

// Hacemos el query
$query = $pdo->prepare("SELECT `CORREO`, `PASSWORD` FROM `asesor` WHERE CORREO=:correo");

// Llenamos campos y ejecutamos
$query->execute([
    'correo' => $myCorreo,
]);

if ($query->rowCount() > 0){

    $check = $query->fetch(PDO::FETCH_ASSOC);
    $row_correo = $check['CORREO'];
    $row_pass = $check['PASSWORD'];

    // Comprobamos el correo iguales
    if($myCorreo == $row_correo){

        if (password_verify($myPass, $row_pass)) {

            echo "¡ÉXITO!";

        } else {

            echo "Su correo o contraseña no coinciden";
        }

    } else {

        echo "Su correo o contraseña no coinciden";

    }
}
```