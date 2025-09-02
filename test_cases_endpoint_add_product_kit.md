# Tabla casos de prueba y pruebas: endpoint añadir productos a la kit

<div style="overflow-x:auto;">
  <table>
  <tr>
    <th>ID</th>
    <th>Título</th>
    <th>Pasos</th>
    <th>Datos de prueba (Cuerpo de la solicitud)</th>
    <th>Resultado esperado</th>
    <th>Resultado actual</th>
    <th>Estado</th>
    <th>Enlace a los informes de errores</th>
  </tr>
    
  <!-- Caso 1 -->
  <tr>
    <td>1</td>
    <td>[POSITIVO] Agregar productos ya existentes a un kit con más de 30 productos distintos (Kit 1: 'Para picnics', 39 productos distintos).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br>
2. En el cuerpo de la solicitud enviar una ID existente de producto 
que ya este en el kit y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=1
2. ID del producto=1
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>Código de respuesta:<br><br>
        400 Bad Request
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-1?atlOrigin=eyJpIjoiOTY0Y2U5ZTM0NTMyNGFkMmJhNzYxMDU4ZWU0MTU3MTQiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 2 -->
  <tr>
    <td>2</td>
    <td>[NEGATIVO] Agregar productos nuevos a un kit predeterminado que ya contiene más de 30 productos distintos (Kit 1: 'Para picnics', 39 productos distintos)</td>
    <td><pre>
1. Envía una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de producto 
que no este en el kit y cantidad de producto.
    </pre></td>
    <td><pre>1. Parámetros de URL=1 
2. ID del producto=71
{
    "productsList": [
        {
            "id": 71,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        400 Bad Request
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
  <!-- Caso 3 -->
  <tr>
    <td>3</td>
    <td>[POSITIVO] Agregar producto a un kit recién creado (kit pasa de 0 a 1 producto distinto).</td>
    <td><pre>
1. Se crea un kit con la solicitud POST /api/v1/kits.<br>   
2. Envíar una solicitud POST a /api/v1/kits/:id/products 
con una ID existente de kit en la URL.<br>  
3. En el cuerpo de la solicitud enviar una ID existente 
de producto y cantidad de producto.
    </pre></td>
    <td><pre>1. Crear Kit
{
    "cardId": 1, 
    "name": "Nuevo Kit"
}
2. ID de URL=7 (kit con 0 productos)
3. ID del producto=1 (producto 1)
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
  <!-- Caso 4 -->
  <tr>
    <td>4</td>
    <td>[POSITIVO] Agregar 29 productos distintos a un kit (límite: 30 productos distintos)</td>
    <td><pre>
1. Envíar tres solicitudes POST a /api/v1/kits/:id/products con una 
ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud agregar 2 productos, enviar una ID 
existente de producto que no este en el kit y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 (kit con 27 productos)
2. ID del producto=1 (producto 28)
    ID del producto=12 (producto 29)
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        },
        {
            "id": 12,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        200 OK 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
  <!-- Caso 5 -->
  <tr>
    <td>5</td>
    <td>[POSITIVO] Agregar 30 productos distintos a un kit (límite permitido).</td>
    <td><pre>
1. Envíar tres solicitudes POST a /api/v1/kits/:id/products con una 
ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud agregar 3 productos, enviar una ID 
existente de producto que no este en el kit y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 (kit con 27 productos)
2. ID del producto=1 (producto 28)
    ID del producto=12 (producto 29)
    ID del producto=13 (producto 30)
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        },
        {
            "id": 12,
            "quantity": 1
        },
        {
            "id": 13,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        200 OK 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
  <!-- Caso 6 -->
  <tr>
    <td>6</td>
    <td>[NEGATIVO] Intentar agregar el producto número 31 a un kit (excede el límite de 30 productos distintos)</td>
    <td><pre>
1. Envíar tres solicitudes POST a /api/v1/kits/:id/products con una 
ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud agregar 4 productos, enviar una ID 
existente de producto que no este en el kit y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 (kit con 27 productos)
2. ID del producto=1 (producto 28)
    ID del producto=12 (producto 29)
    ID del producto=13 (producto 30)
    ID del producto=14 (producto 31)
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        },
        {
            "id": 12,
            "quantity": 1
        },
        {
            "id": 13,
            "quantity": 1
        },
        {
            "id": 14,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        400 Bad Request
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
  <!-- Caso 7 -->
  <tr>
    <td>7</td>
    <td>[NEGATIVO] Intentar agregar un producto sin el campo 'ID' a un kit (falta key:value en el payload).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con 
una ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud se borra key:value del ID del 
producto y se agrega la cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. 
{
    "productsList": [
        {
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-2?atlOrigin=eyJpIjoiOGRkNDdiOWE2NTA2NGRmYmFiMDhiNDBiOTk1NGQ5MzIiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 8 -->
  <tr>
    <td>8</td>
    <td>[NEGATIVO] Intentar agregar un producto sin el campo 'cantidad' a un kit (falta key:value en el payload).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con 
una ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de 
producto y se borra key:value de la cantidad del producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. ID del producto 1
{
    "productsList": [
        {
            "id": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        500 Internal Server Error<br><br>
        Cuerpo de respuesta:<br><br>
        "message": "invalid input syntax for integer"<br><br>
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-3?atlOrigin=eyJpIjoiYjRmM2Q3Mjc0ZDg3NDMyYjk1ZTczM2JjODZmMzA0MTIiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 9 -->
  <tr>
    <td>9</td>
    <td>[NEGATIVO] Intentar agregar un producto a un kit inexistente (ID de kit inválido o no registrado).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con 
una ID inexistente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de 
producto y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=100 
2. ID del producto 1
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        404 Not found 
    </td>
    <td>Código de respuesta:<br><br>
        404 Not found
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
  <!-- Caso 10 -->
  <tr>
    <td>10</td>
    <td>[NEGATIVO] Intentar agregar un producto con ID no registrado a un kit (producto inexistente).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products 
con una ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID inexistente 
de producto y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. ID del producto 0
{
    "productsList": [
        {
            "id": 0,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-4?atlOrigin=eyJpIjoiOThjYmQzNWY1NTdlNGM5ODkwZDUwYzdkM2JhZGIzODAiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 11 -->
  <tr>
    <td>11</td>
    <td>[NEGATIVO] Intentar agregar un producto con ID null o vacío a un kit (validación de campos obligatorios).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con 
una ID existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar un dato de tipo "Null o 
vacio" en ID de producto y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. ID del producto=null
{
    "productsList": [
        {
            "id": null,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-5?atlOrigin=eyJpIjoiMjE1YzdiMzM2ZTBlNGEyOWExNmFiNzEzNGZjZjExMjQiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 12 -->
  <tr>
    <td>12</td>
    <td>[NEGATIVO] Intentar agregar un producto con cantidad null o vacía a un kit (validación de campos obligatorios).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de producto 
y se ingresa un dato tipo "Null o vacio" en cantidad del producto.
    </pre></td>
    <td><pre>1. Parámetros de ruta: id=2
2. ID del producto=1 y cantidad=null 
{
    "productsList": [
        {
            "id": 1,
            "quantity": null
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-6?atlOrigin=eyJpIjoiZmRmODgzOGUyMjQ1NDI5YmJlZTJhODRlMTUyZDNmYjciLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 13 -->
  <tr>
    <td>13</td>
    <td>[NEGATIVO] Intentar agregar un producto con ID de tipo string a un kit (validación de tipo de dato).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar un dato de tipo "string" en 
ID de producto y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. ID del producto="Hl"
{
    "productsList": [
        {
            "id": "HI",
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td><pre>
Código de respuesta:
500 Internal Server Error&lt;br&gt;
Cuerpo de respuesta:
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;Error&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;pre&gt;Internal Server Error&lt;/pre&gt;
&lt;/body&gt;
&lt;/html&gt;
    </pre></td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-7?atlOrigin=eyJpIjoiY2YwZTk2YWY4ZDJiNDM1N2FjNzk3ZTFlZTdhZWYzNjMiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 14 -->
  <tr>
    <td>14</td>
    <td>[NEGATIVO] Intentar agregar un producto con cantidad de tipo string a un kit (validación de tipo de dato).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de producto 
y se ingresa un dato tipo "string" en cantidad del producto.
    <td><pre>1. Parámetros de ruta: id=2
2. ID del producto=1 y cantidad="HI"
{
    "productsList": [
        {
            "id": 1,
            "quantity": "HI"
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        500 Internal Server Error<br><br>
        Cuerpo de respuesta:<br><br>
        "message": "invalid input syntax for integer"<br><br>
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-30?atlOrigin=eyJpIjoiYThhYmRkYjU3ZTAzNGYyYTkzYjM5MDE1Mzc1YmZiMTgiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 15 -->
  <tr>
    <td>15</td>
    <td>[NEGATIVO] Intentar agregar un producto con ID de tipo boolean a un kit (validación de tipo de dato).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar un dato de tipo "booleano" 
en ID de producto y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. ID del producto=true
{
    "productsList": [
        {
            "id": true,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td><pre>
Código de respuesta:
500 Internal Server Error&lt;br&gt;
Cuerpo de respuesta:
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;Error&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;pre&gt;Internal Server Error&lt;/pre&gt;
&lt;/body&gt;
&lt;/html&gt;
    </pre></td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-8?atlOrigin=eyJpIjoiNjE0NjI2OThhZjQ3NDQwM2JmOGNhM2VmOTcxZmU2NzgiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 16 -->
  <tr>
    <td>16</td>
    <td>[NEGATIVO] Intentar agregar un producto con cantidad de tipo boolean a un kit (validación de tipo de dato).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de producto 
y se ingresa un dato tipo "booleano" en cantidad del producto.
    <td><pre>1. Parámetros de ruta: id=2
2. ID del producto=1 y cantidad=true 
{
    "productsList": [
        {
            "id": 1,
            "quantity": true
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK 
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-9?atlOrigin=eyJpIjoiYTJlYjE5MTE1NWM0NGUzYWIzZmMwNWE1NmJlNDQ0YTkiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 17 -->
  <tr>
    <td>17</td>
    <td>[NEGATIVO] Intentar agregar un producto con ID de tipo float a un kit (validación de tipo de dato).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar un dato de tipo "float" en 
ID de producto y cantidad de producto.
    </pre></td>
    <td><pre>1. ID de URL=2 
2. ID del producto=1.5
{
    "productsList": [
        {
            "id": 1.5,
            "quantity": 1
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td><pre>
Código de respuesta:
500 Internal Server Error&lt;br&gt;
Cuerpo de respuesta:
&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="utf-8"&gt;
    &lt;title&gt;Error&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;pre&gt;Internal Server Error&lt;/pre&gt;
&lt;/body&gt;
&lt;/html&gt;
    </pre></td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-10?atlOrigin=eyJpIjoiZTlkZjkwNGQ2ZjNlNDY0OTgwNWM5MjY3ZDMzZWNlOGYiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 18 -->
  <tr>
    <td>18</td>
    <td>[NEGATIVO] Intentar agregar un producto con cantidad de tipo float a un kit (validación de tipo de dato).</td>
    <td><pre>
1. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
2. En el cuerpo de la solicitud enviar una ID existente de producto 
y se ingresa un dato tipo "float" en cantidad del producto.
    <td><pre>1. Parámetros de ruta: id=2
2. ID del producto=1 y cantidad=1.5 
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1.5
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        400 Bad Request 
    </td>
    <td>Código de respuesta:<br><br>
        500 Internal Server Error<br><br>
        Cuerpo de respuesta:<br><br>
        "message": "invalid input syntax for integer"<br><br>
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-31?atlOrigin=eyJpIjoiOGZjNWI1ZjZkYTA0NGQzYWE5YTkxZjFmMzk4NmRjNmUiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 19 -->
  <tr>
    <td>19</td>
    <td>[POSITIVO] Agregar 2 cantidades del mismo producto a un kit por separado.</td>
    <td><pre>
1. Se crea un kit con la solicitud POST /api/v1/kits.<br>   
2. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
3. En el cuerpo de la solicitud enviar los dos productos con la 
misma ID de producto y cantidad de producto.
    <td><pre>1. Parámetros de ruta: id=7
2. ID del producto=1 y cantidad 1 y 50 
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        },
       {
            "id": 1,
            "quantity": 50
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        200 OK <br><br>
        En el cuerpo de respuesta se agrega 51 cantidades producto 
    </td>
    <td>Código de respuesta:<br><br>
        200 OK <br><br>
        En el cuerpo de respuesta solo se agrega 1 cantidad de producto (primero que se agrego).
    </td>
    <td>NO APROBADO</td>
    <td><a href="https://yostinch.atlassian.net/browse/IES4-11?atlOrigin=eyJpIjoiYjIzNTA4YWQ5OGFmNDNmNGE1OTAzYTJhYWFkMDQ0ZjIiLCJwIjoiaiJ9" target="_blank">Link a Jira</a></td>
  </tr>
  <!-- Caso 20 -->
  <tr>
    <td>20</td>
    <td>[POSITIVO] Agregar 2 cantidades del mismo producto a un kit por separado.</td>
    <td><pre>
1. Se crea un kit con la solicitud POST /api/v1/kits.<br>   
2. Envíar una solicitud POST a /api/v1/kits/:id/products con una ID 
existente de kit en la URL.<br> 
3. En el cuerpo de la solicitud enviar los dos productos con distinta 
ID de producto y cantidad de producto.
    <td><pre>1. Parámetros de ruta: id=7
2. ID del producto=1 y cantidad 1 y 50 
{
    "productsList": [
        {
            "id": 1,
            "quantity": 1
        },
       {
            "id": 2,
            "quantity": 50
        }
    ]
}
    </pre></td>
    <td>Código de respuesta:<br><br>
        200 OK
    </td>
    <td>Código de respuesta:<br><br>
        200 OK 
    </td>
    <td>APROBADO</td>
    <td></td>
  </tr>
</table>

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
 

























