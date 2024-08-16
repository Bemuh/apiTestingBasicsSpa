# Casos de Prueba de API y Ejemplos de Ejecución en Postman

## 1. Verificar que el código de estado de la respuesta de la API es 200 OK.
**Objetivo:** Asegurarse de que la API está respondiendo correctamente a las solicitudes y que la comunicación es exitosa.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

## 2. Verificar que la respuesta de la API está en el formato esperado (ej., JSON, XML).
**Objetivo:** Validar que la API devuelve datos en el formato correcto, asegurando que los consumidores de la API puedan procesar la respuesta adecuadamente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response is JSON", function () {
    pm.response.to.be.json;
});
```

## 3. Verificar que la respuesta de la API contiene todos los campos esperados.
**Objetivo:** Confirmar que la respuesta de la API incluye todos los campos obligatorios, garantizando que la información devuelta es completa y usable.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response has expected fields", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('campo1');
    pm.expect(jsonData).to.have.property('campo2');
});
```

## 4. Verificar que la respuesta de la API contiene los datos correctos para cada campo.
**Objetivo:** Asegurar que la información devuelta por la API es precisa y coincide con los datos esperados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response has correct data", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.campo1).to.eql('valor_esperado');
    pm.expect(jsonData.campo2).to.eql('valor_esperado');
});
```

## 5. Verificar que el tiempo de respuesta de la API está dentro de los límites aceptables.
**Objetivo:** Comprobar que la API responde dentro de un marco de tiempo razonable, lo cual es crucial para la experiencia del usuario y la eficiencia del sistema.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response time is acceptable", function () {
    pm.expect(pm.response.responseTime).to.be.below(2000); // Tiempo en milisegundos
});
```

## 6. Verificar que los parámetros de la solicitud a la API se pasan correctamente.
**Objetivo:** Asegurarse de que los parámetros enviados en la solicitud son recibidos y procesados correctamente por la API.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso?parametro1=valor1&parametro2=valor2`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Query params are correct", function () {
    pm.expect(pm.request.url.query.toObject()).to.include({parametro1: 'valor1', parametro2: 'valor2'});
});
```

## 7. Verificar que el método de solicitud a la API es correcto (ej., GET, POST, PUT, DELETE).
**Objetivo:** Validar que la solicitud está utilizando el método HTTP correcto, acorde con las expectativas del endpoint.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Request method is POST", function () {
    pm.expect(pm.request.method).to.eql('POST');
});
```

## 8. Verificar que la URL del endpoint de la API es correcta.
**Objetivo:** Asegurarse de que la solicitud se está realizando al endpoint correcto, evitando errores en la interacción con la API.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Endpoint URL is correct", function () {
    pm.expect(pm.request.url.toString()).to.eql('https://api.ejemplo.com/recurso');
});
```

## 9. Verificar que los encabezados de la respuesta de la API son correctos.
**Objetivo:** Validar que los encabezados HTTP en la respuesta son los esperados, asegurando la correcta interpretación de los datos devueltos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Headers are correct", function () {
    pm.response.to.have.header("Content-Type", "application/json");
});
```

## 10. Verificar que el tamaño de la carga útil de la respuesta de la API está dentro de los límites aceptables.
**Objetivo:** Asegurarse de que el tamaño de la respuesta es manejable y no excede los límites que podrían afectar el rendimiento o la usabilidad.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Payload size is acceptable", function () {
    var responseSize = pm.response.headers.get('Content-Length');
    pm.expect(parseInt(responseSize)).to.be.below(5000); // Tamaño en bytes
});
```

## 11. Verificar que la API devuelve un mensaje de error si la solicitud está mal formada.
**Objetivo:** Confirmar que la API maneja adecuadamente las solicitudes mal formadas y devuelve mensajes de error claros y correctos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Cuerpo: `{malformado:}`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Error on malformed request", function () {
    pm.response.to.have.status(400);
});
```

## 12. Verificar que la API devuelve un mensaje de error si la autenticación falla.
**Objetivo:** Asegurarse de que la API requiere y valida correctamente las credenciales de autenticación, y maneja los errores de autenticación de manera adecuada.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Encabezado: `Authorization: Bearer token_incorrecto`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Authentication fails", function () {
    pm.response.to.have.status(401);
});
```

## 13. Verificar que la API devuelve un mensaje de error si la carga útil de la solicitud falta.
**Objetivo:** Validar que la API responde con un error apropiado cuando se omite la carga útil necesaria en una solicitud.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Cuerpo: **Vacío**
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Error on missing payload", function () {
    pm.response.to.have.status(400);
});
```

## 14. Verificar que la API devuelve un mensaje de error si el recurso solicitado no existe.
**Objetivo:** Asegurarse de que la API maneja correctamente las solicitudes para recursos inexistentes, devolviendo el código de estado adecuado.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso_no_existente`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Resource does not exist", function () {
    pm.response.to.have.status(404);
});
```

## 15. Verificar que la API devuelve un mensaje de error si el recurso solicitado no está autorizado.
**Objetivo:** Validar que la API maneja correctamente las solicitudes a recursos para los cuales el usuario no tiene autorización, devolviendo el código de error adecuado.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso_privado`
- Encabezado: `Authorization: Bearer token_incorrecto`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Resource is unauthorized", function () {
    pm.response.to.have.status(403);
});
```

## 16. Verificar que la API devuelve un mensaje de error si la carga útil de la solicitud excede el límite permitido.
**Objetivo:** Asegurarse de que la API limita correctamente el tamaño de la carga útil en las solicitudes y devuelve un error si se excede.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Cuerpo: **JSON grande que excede el límite**
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Payload exceeds limit", function () {
    pm.response.to.have.status(413);
});
```

## 17. Verificar que la API devuelve un mensaje de error si la carga útil de la solicitud contiene datos inválidos.
**Objetivo:** Confirmar que la API valida correctamente los datos de entrada y devuelve errores cuando los datos no son válidos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Cuerpo: `{campo: "valor_invalido"}`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Invalid data in request", function () {
    pm.response.to.have.status(422);
});
```

## 18. Verificar que la API devuelve un mensaje de error si el método de solicitud no está permitido para el recurso.
**Objetivo:** Validar que la API responde con el error adecuado cuando se utiliza un método HTTP no permitido para un recurso específico.
**Ejemplo en Postman:**
- Método: `DELETE`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Method not allowed", function () {
    pm.response.to.have.status(405);
});
```

## 19. Verificar que la API devuelve un mensaje de éxito si el recurso se crea correctamente.
**Objetivo:** Asegurarse de que la API maneja correctamente la creación de recursos y devuelve una confirmación de éxito.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Cuerpo: `{campo: "valor_correcto"}`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Resource created successfully", function () {
    pm.response.to.have.status(201);
});
```

## 20. Verificar que la API devuelve un mensaje de éxito si el recurso se actualiza correctamente.
**Objetivo:** Confirmar que la API puede actualizar recursos existentes y proporciona una respuesta de éxito.
**Ejemplo en Postman:**
- Método: `PUT`
- URL: `https://api.ejemplo.com/recurso/1`
- Cuerpo: `{campo: "valor_actualizado"}`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Resource updated successfully", function () {
    pm.response.to.have.status(200);
});
```

## 21. Verificar que la API devuelve un mensaje de éxito si el recurso se elimina correctamente.
**Objetivo:** Validar que la API maneja correctamente la eliminación de recursos y devuelve una confirmación adecuada.
**Ejemplo en Postman:**
- Método: `DELETE`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Resource deleted successfully", function () {
    pm.response.to.have.status(204);
});
```

## 22. Verificar que la API devuelve un mensaje de éxito si el recurso se recupera correctamente.
**Objetivo:** Asegurarse de que la API puede recuperar recursos existentes y proporciona la respuesta adecuada.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Resource retrieved successfully", function () {
    pm.response.to.have.status(200);
});
```

## 23. Verificar que la API devuelve el recurso correcto basado en el identificador de recurso proporcionado.
**Objetivo:** Confirmar que la API devuelve el recurso específico solicitado utilizando un identificador único.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct resource returned", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.id).to.eql(1);
});
```

## 24. Verificar que la API devuelve el recurso correcto basado en los parámetros de búsqueda proporcionados.
**Objetivo:** Asegurarse de que la API puede filtrar y devolver recursos basados en criterios de búsqueda específicos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso?nombre=ejemplo`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct resource returned based on search", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.nombre).to.eql('ejemplo');
});
```

## 25. Verificar que la respuesta de la API contiene la información de paginación correcta.
**Objetivo:** Validar que la API maneja correctamente la paginación y que la información devuelta refleja los parámetros de paginación solicitados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?page=1&limit=10`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Pagination info is correct", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.page).to.eql(1);
    pm.expect(jsonData.limit).to.eql(10);
});
```

## 26. Verificar que la respuesta de la API contiene el orden de clasificación correcto basado en el parámetro de orden proporcionado.
**Objetivo:** Asegurarse de que la API clasifica correctamente los recursos de acuerdo con el parámetro de orden solicitado.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?sort=nombre`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Sorting order is correct", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData[0].nombre).to.eql('Alfa');
    pm.expect(jsonData[jsonData.length - 1].nombre).to.eql('Omega');
});
```

## 27. Verificar que la respuesta de la API contiene la información de filtrado correcta basada en los parámetros de filtro proporcionados.
**Objetivo:** Validar que la API puede filtrar los recursos correctamente según los criterios de filtrado proporcionados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?filtro=activo`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Filtering info is correct", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.every(function(item) { return item.activo === true; })).to.be.true;
});
```

## 28. Verificar que la API devuelve los resultados correctos al buscar una cadena parcial.
**Objetivo:** Asegurarse de que la API puede manejar búsquedas con cadenas parciales y devolver resultados que coincidan.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=par`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Partial string search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('par'); })).to.be.true;
});
```

## 29. Verificar que la API devuelve los resultados correctos al buscar una cadena sin distinción entre mayúsculas y minúsculas.
**Objetivo:** Validar que la API realiza búsquedas de manera insensible a mayúsculas/minúsculas y devuelve los resultados adecuados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=EJEMPLO`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Case-insensitive search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.toLowerCase() === 'ejemplo'; })).to.be.true;
});
```

## 30. Verificar que la API devuelve los resultados correctos al buscar una cadena con caracteres especiales.
**Objetivo:** Asegurarse de que la API puede manejar cadenas con caracteres especiales en las búsquedas y devolver resultados adecuados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=%24pecial`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Special characters search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('$pecial'); })).to.be.true;
});
```

## 31. Verificar que la API devuelve los resultados correctos al buscar una cadena con múltiples palabras.
**Objetivo:** Confirmar que la API maneja correctamente las búsquedas con múltiples palabras y devuelve los resultados esperados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=dos+palabras`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multiple words search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('dos palabras'); })).to.be.true;
});
```

## 32. Verificar que la API devuelve los resultados correctos al buscar una cadena con una combinación de letras y números.
**Objetivo:** Asegurarse de que la API puede manejar búsquedas con cadenas mixtas de letras y números, devolviendo los resultados correctos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=letras123`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Letters and numbers search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('letras123'); })).to.be.true;
});
```

## 33. Verificar que la API devuelve los resultados correctos al buscar una cadena con espacios.
**Objetivo:** Validar que la API maneja correctamente las búsquedas con cadenas que contienen espacios y devuelve los resultados esperados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=una%20frase`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Search with spaces returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('una frase'); })).to.be.true;
});
```

## 34. Verificar que la API devuelve los resultados correctos al buscar una cadena con caracteres no ASCII.
**Objetivo:** Asegurarse de que la API puede manejar correctamente caracteres no ASCII en las búsquedas y devolver los resultados correctos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=café`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Non-ASCII characters search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('café'); })).to.be.true;
});
```

## 35. Verificar que la API devuelve los resultados correctos al buscar una cadena con tipos de caracteres mixtos (ej., letras, números, símbolos).
**Objetivo:** Validar que la API puede manejar búsquedas con combinaciones de diferentes tipos de caracteres y devolver los resultados adecuados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=A1b2#`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Mixed character types search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('A1b2#'); })).to.be.true;
});
```

## 36. Verificar que la API devuelve los resultados correctos al buscar una cadena con etiquetas HTML.
**Objetivo:** Asegurarse de que la API puede procesar correctamente cadenas que incluyen etiquetas HTML en las búsquedas.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=%3Ch1%3ETitulo%3C%2Fh1%3E`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("HTML tags search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.descripcion.includes('<h1>Titulo</h1>'); })).to.be.true;
});
```

## 37. Verificar que la API devuelve los resultados correctos al buscar una cadena con caracteres de escape.
**Objetivo:** Validar que la API maneja correctamente las cadenas con caracteres de escape en las búsquedas, devolviendo resultados precisos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recursos?buscar=escape%5Cnueva%20linea`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Escape characters search returns correct results", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.some(function(item) { return item.nombre.includes('escape\nueva linea'); })).to.be.true;
});
```

## 38. Verificar que la respuesta de la API contiene la representación correcta del recurso basada en el tipo de contenido proporcionado.
**Objetivo:** Asegurarse de que la API devuelve los datos en el formato solicitado, basado en los encabezados de tipo de contenido proporcionados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept: application/json`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct content type returned", function () {
    pm.response.to.have.header("Content-Type", "application/json");
});
```

## 39. Verificar que la respuesta de la API está comprimida cuando el cliente envía una solicitud con el encabezado "Accept-Encoding" configurado en "gzip".
**Objetivo:** Validar que la API soporta y responde con compresión gzip cuando es solicitado por el cliente, mejorando la eficiencia de la transmisión de datos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept-Encoding: gzip`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response is compressed", function () {
    pm.response.to.have.header("Content-Encoding", "gzip");
});
```

## 40. Verificar que la respuesta de la API no está comprimida cuando el cliente no envía el encabezado "Accept-Encoding".
**Objetivo:** Asegurarse de que la API no comprime la respuesta si no se solicita, respetando los encabezados de solicitud del cliente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: Ninguno
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response is not compressed", function () {
    pm.response.to.not.have.header("Content-Encoding");
});
```

## 41. Verificar que la respuesta de la API no está comprimida cuando el cliente envía una solicitud con el encabezado "Accept-Encoding" configurado a un valor diferente de "gzip".
**Objetivo:** Confirmar que la API maneja correctamente la compresión basada en las preferencias del cliente, evitando la compresión si no se solicita "gzip".
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept-Encoding: deflate`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response is not compressed with non-gzip encoding", function () {
    pm.response.to.not.have.header("Content-Encoding", "gzip");
});
```

## 42. Verificar que la respuesta de la API contiene la representación correcta del recurso basada en el idioma especificado (por ejemplo, inglés, español, francés).
**Objetivo:** Asegurarse de que la API responde en el idioma correcto según lo especificado en la solicitud, proporcionando contenido localizado.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept-Language: es`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct language resource returned", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.idioma).to.eql('es');
});
```

## 43. Verificar que la respuesta de la API contiene la representación correcta del recurso basada en la configuración regional especificada (por ejemplo, en-US, fr-FR).
**Objetivo:** Validar que la API responde adecuadamente a las solicitudes con diferentes configuraciones regionales, proporcionando contenido específico de la región.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept-Language: en-US`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct locale resource returned", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.locale).to.eql('en-US');
});
```

## 44. Verificar que la respuesta de la API contiene la representación correcta del recurso basada en la zona horaria especificada.
**Objetivo:** Asegurarse de que la API responde con la información correcta de zona horaria cuando se especifica, adaptando los datos a la zona horaria solicitada.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Time-Zone: America/New_York`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct timezone resource returned", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.timezone).to.eql('America/New_York');
});
```

## 45. Verificar que la respuesta de la API contiene la representación correcta del recurso cuando el recurso contiene objetos o arreglos anidados.
**Objetivo:** Validar que la API puede manejar y devolver correctamente estructuras de datos anidadas, como objetos y arreglos dentro de la respuesta.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Nested objects/arrays handled correctly", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.detalles[0].atributo).to.eql('valor');
});
```

## 46. Verificar que la API devuelve una respuesta dentro de un período de tiempo especificado.
**Objetivo:** Asegurarse de que la API es capaz de responder rápidamente dentro de los límites de tiempo establecidos, mejorando la experiencia del usuario.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response received within time limit", function () {
    pm.expect(pm.response.responseTime).to.be.below(500); // 500ms
});
```

## 47. Verificar que la API maneja correctamente las solicitudes concurrentes.
**Objetivo:** Validar que la API puede manejar múltiples solicitudes simultáneas sin errores, garantizando la integridad de los datos y el rendimiento.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: Realizar múltiples solicitudes simultáneas en Postman y en la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Concurrent requests handled correctly", function () {
    pm.expect(pm.response).to.have.status(200);
});
```

## 48. Verificar que la API maneja correctamente las actualizaciones parciales (por ejemplo, solicitudes PATCH).
**Objetivo:** Asegurarse de que la API puede procesar y aplicar correctamente actualizaciones parciales a los recursos.
**Ejemplo en Postman:**
- Método: `PATCH`
- URL: `https://api.ejemplo.com/recurso/1`
- Body: 
```javascript
{
    "atributo": "nuevo valor"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Partial update successful", function () {
    pm.response.to.have.status(200);
});
```

## 49. Verificar que la API devuelve una respuesta con un encabezado HTTP personalizado cuando se envía un encabezado de solicitud específico.
**Objetivo:** Validar que la API reconoce y responde con los encabezados HTTP personalizados cuando se solicitan, confirmando la flexibilidad en la comunicación.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `X-Custom-Header: valor`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Custom header response received", function () {
    pm.response.to.have.header("X-Custom-Response-Header");
});
```

## 50. Verificar que la API maneja correctamente las cargas y descargas de archivos.
**Objetivo:** Asegurarse de que la API puede manejar correctamente la subida y bajada de archivos, incluyendo el manejo de grandes cantidades de datos binarios.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/upload`
- Body: Seleccionar `form-data` y agregar un campo de tipo archivo.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("File upload handled correctly", function () {
    pm.response.to.have.status(201);
});
```

## 51. Verificar que la respuesta de la API contiene la representación correcta del recurso basada en la moneda especificada.
**Objetivo:** Validar que la API responde correctamente con datos financieros en la moneda especificada por el cliente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Currency: USD`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Correct currency resource returned", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.moneda).to.eql('USD');
});
```

## 52. Verificar que la API maneja correctamente la limitación de velocidad y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API implementa políticas de limitación de velocidad para evitar abusos y gestionar el tráfico de manera eficiente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar múltiples solicitudes rápidamente.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Rate limiting handled correctly", function () {
    pm.response.to.have.status(429);
});
```

## 53. Verificar que la API maneja correctamente los reintentos y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API maneja correctamente los reintentos de solicitudes, especialmente en casos de errores temporales, sin causar inconsistencias.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar una solicitud que provoque un error temporal y luego un reintento.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Retries handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 54. Verificar que la API maneja correctamente las redirecciones y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API sigue correctamente las redirecciones y devuelve el código de estado apropiado, gestionando los cambios de ubicación de los recursos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/redirect`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Redirect handled correctly", function () {
    pm.response.to.have.status(301);
});
```

## 55. Verificar que la API maneja correctamente las cookies y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API gestiona correctamente las cookies, incluyéndolas en la respuesta cuando es necesario, para mantener la sesión o la autenticación.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Cookies handled correctly", function () {
    pm.response.to.have.cookie("session_id");
});
```

## 56. Verificar que la API maneja correctamente el almacenamiento en caché y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API implementa políticas de caché adecuadas para mejorar el rendimiento y reducir la carga del servidor.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Caching handled correctly", function () {
    pm.response.to.have.header("Cache-Control");
});
```

## 57. Verificar que la API maneja correctamente los tokens CSRF y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API protege contra ataques CSRF asegurándose de que los tokens CSRF se manejan correctamente en las solicitudes.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `X-CSRF-Token: token`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("CSRF token handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 58. Verificar que la API maneja correctamente los ataques de secuencias de comandos entre sitios (XSS) y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API es segura contra ataques XSS al validar y sanitizar adecuadamente los datos de entrada.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Body: 
```javascript
{
    "script": "<script>alert('xss')</script>"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("XSS attack prevented", function () {
    pm.response.to.have.status(400);
});
```

## 59. Verificar que la API maneja correctamente los ataques de inyección SQL y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API está protegida contra ataques de inyección SQL, asegurando que las entradas no controladas no puedan alterar las consultas de la base de datos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Body: 
```javascript
{
    "consulta": "SELECT * FROM usuarios WHERE nombre = 'admin' --"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("SQL injection attack prevented", function () {
    pm.response.to.have.status(400);
});
```

## 60. Verificar que la API maneja correctamente los ataques de falsificación de solicitudes entre sitios (CSRF) y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API está protegida contra ataques CSRF, validando que solo se procesan solicitudes legítimas con tokens CSRF válidos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `X-CSRF-Token: token`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("CSRF attack prevented", function () {
    pm.response.to.have.status(200);
});
```

## 61. Verificar que la API maneja correctamente la validación de entradas y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API valida correctamente las entradas antes de procesarlas, evitando la inserción de datos inválidos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "valor inválido"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Input validation handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 62. Verificar que la API maneja correctamente la codificación de salidas y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API codifica correctamente las salidas, asegurando que los datos devueltos están en el formato esperado y seguro.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Output encoding handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 63. Verificar que la API maneja correctamente los certificados SSL/TLS y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API utiliza y valida correctamente los certificados SSL/TLS para proteger la comunicación entre el cliente y el servidor.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("SSL/TLS certificates handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 64. Verificar que la API maneja correctamente la negociación de contenido y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API puede negociar el tipo de contenido solicitado por el cliente, devolviendo el formato correcto de datos (JSON, XML, etc.).
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept: application/json`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Content negotiation handled correctly", function () {
    pm.response.to.have.status(200);
    pm.response.to.be.json;
});
```

## 65. Verificar que la API maneja correctamente la autenticación y autorización y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API gestiona correctamente la autenticación y autorización, permitiendo el acceso solo a usuarios autorizados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/privado`
- Headers: `Authorization: Bearer <token>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Authentication and authorization handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 66. Verificar que la API maneja correctamente la limitación de solicitudes y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API impone correctamente límites en la cantidad de solicitudes permitidas por usuario o IP, protegiendo contra abusos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar múltiples solicitudes rápidamente.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Rate limiting handled correctly", function () {
    pm.response.to.have.status(429);
});
```

## 67. Verificar que la API maneja correctamente los intentos de reintento y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API maneja correctamente los intentos de reintento después de fallos temporales, garantizando la fiabilidad del servicio.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar una solicitud que provoque un error temporal y luego un reintento.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Retries handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 68. Verificar que la API maneja correctamente los tiempos de espera y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API gestiona correctamente los tiempos de espera, asegurando que las solicitudes no queden colgadas y devuelvan respuestas adecuadas.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Timeout handled correctly", function () {
    pm.expect(pm.response.responseTime).to.be.below(3000); // 3 segundos
});
```

## 69. Verificar que la API maneja correctamente los fallos de red y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API maneja adecuadamente los fallos de red, devolviendo respuestas de error correctas y evitando colapsos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Simular un fallo de red en Postman.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Network failure handled correctly", function () {
    pm.response.to.have.status(503);
});
```

## 70. Verificar que la API maneja correctamente las condiciones de carrera y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API puede manejar situaciones donde múltiples solicitudes intentan modificar el mismo recurso simultáneamente, sin causar inconsistencias.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar solicitudes concurrentes para modificar el mismo recurso.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Race conditions handled correctly", function () {
    pm.response.to.have.status(409);
});
```

## 71. Verificar que la API maneja correctamente el almacenamiento en caché y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API implementa políticas de caché adecuadas para mejorar el rendimiento y reducir la carga del servidor.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Caching handled correctly", function () {
    pm.response.to.have.header("Cache-Control");
});
```

## 72. Verificar que la API maneja correctamente el versionado y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API soporta el versionado, permitiendo a los clientes acceder a diferentes versiones de los recursos según sea necesario.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/v1/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Versioning handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 73. Verificar que la API maneja correctamente la negociación de versiones y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API puede negociar y responder con la versión correcta de un recurso cuando se solicita una versión específica.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept-Version: 1.0`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Version negotiation handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 74. Verificar que la API maneja correctamente la negociación de contenido y devuelve el código de estado HTTP correcto.
**Objetivo:** Validar que la API puede negociar el tipo de contenido solicitado por el cliente, devolviendo el formato correcto de datos (JSON, XML, etc.).
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Headers: `Accept: application/xml`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Content negotiation handled correctly", function () {
    pm.response.to.have.status(200);
    pm.response.to.be.xml;
});
```

## 75. Verificar que la API maneja correctamente las actualizaciones parciales y devuelve el código de estado HTTP correcto.
**Objetivo:** Asegurarse de que la API puede procesar y aplicar correctamente actualizaciones parciales a los recursos.
**Ejemplo en Postman:**
- Método: `PATCH`
- URL: `https://api.ejemplo.com/recurso/1`
- Body: 
```javascript
{
    "campo": "nuevo valor"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Partial update handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 76. Verificar que la API maneja correctamente las condiciones de error y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API responde adecuadamente a situaciones de error, proporcionando mensajes claros y correctos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/404`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Error conditions handled correctly", function () {
    pm.response.to.have.status(404);
    pm.expect(pm.response.text()).to.include("Not Found");
});
```

## 77. Verificar que la API maneja correctamente varios tipos de solicitudes, como GET, POST, PUT, DELETE, OPTIONS, HEAD, y PATCH.
**Objetivo:** Asegurarse de que la API puede manejar todos los métodos HTTP soportados, respondiendo correctamente a cada tipo de solicitud.
**Ejemplo en Postman:**
- Método: `OPTIONS`
- URL: `https://api.ejemplo.com/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Various request methods handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 78. Verificar que la API maneja correctamente varios tipos de datos, como cadenas, números, fechas y datos binarios.
**Objetivo:** Validar que la API puede procesar correctamente diferentes tipos de datos, garantizando la consistencia y exactitud en la manipulación de estos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "cadena": "texto",
    "numero": 123,
    "fecha": "2024-08-16",
    "binario": "SGVsbG8gd29ybGQ="
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Various data types handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 79. Verificar que la API maneja correctamente varios tipos de autenticación, como autenticación básica, autenticación por token y OAuth.
**Objetivo:** Asegurarse de que la API puede manejar diferentes esquemas de autenticación, garantizando la seguridad y control de acceso adecuado.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/privado`
- Headers: `Authorization: Bearer <token>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Various authentication types handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 80. Verificar que la API maneja correctamente varios tipos de autorización, como basado en roles.
**Objetivo:** Validar que la API puede gestionar diferentes niveles de permisos y roles, asegurando que solo los usuarios autorizados tienen acceso a los recursos correspondientes.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/privado`
- Headers: `Authorization: Bearer <token>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Role-based authorization handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 81. Verificar que la API devuelve el código de estado HTTP correcto para solicitudes que no son compatibles (por ejemplo, HTTP 405 Method Not Allowed).
**Objetivo:** Asegurarse de que la API maneja correctamente las solicitudes no permitidas para ciertos recursos, devolviendo el código de estado adecuado.
**Ejemplo en Postman:**
- Método: `DELETE`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("405 Method Not Allowed handled correctly", function () {
    pm.response.to.have.status(405);
});
```

## 82. Verificar que la API devuelve el código de estado HTTP correcto para solicitudes inválidas (por ejemplo, HTTP 400 Bad Request).
**Objetivo:** Validar que la API identifica y responde adecuadamente a las solicitudes mal formadas o inválidas, devolviendo el error correcto.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": ""
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("400 Bad Request handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 83. Verificar que la API devuelve el código de estado HTTP correcto para solicitudes no autorizadas (por ejemplo, HTTP 401 Unauthorized).
**Objetivo:** Asegurarse de que la API maneja correctamente las solicitudes que requieren autenticación, devolviendo el código de estado apropiado cuando las credenciales son incorrectas o faltan.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/privado`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("401 Unauthorized handled correctly", function () {
    pm.response.to.have.status(401);
});
```

## 84. Verificar que la API devuelve el código de estado HTTP correcto para solicitudes prohibidas (por ejemplo, HTTP 403 Forbidden).
**Objetivo:** Validar que la API responde con el código de estado adecuado cuando se intenta acceder a un recurso sin los permisos necesarios.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/prohibido`
- Headers: `Authorization: Bearer <token>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("403 Forbidden handled correctly", function () {
    pm.response.to.have.status(403);
});
```

## 85. Verificar que la API devuelve el código de estado HTTP correcto para recursos no encontrados (por ejemplo, HTTP 404 Not Found).
**Objetivo:** Asegurarse de que la API maneja adecuadamente las solicitudes para recursos que no existen, devolviendo el código de estado correspondiente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/no-existente`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("404 Not Found handled correctly", function () {
    pm.response.to.have.status(404);
});
```

## 86. Verificar que la API maneja correctamente la paginación y devuelve los recursos correctos para cada página.
**Objetivo:** Validar que la API implementa correctamente la paginación, permitiendo a los clientes acceder a secciones específicas de un gran conjunto de datos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso?page=2`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Pagination handled correctly", function () {
    pm.response.to.have.status(200);
    pm.expect(pm.response.json()).to.have.property("page", 2);
});
```

## 87. Verificar que la API maneja correctamente la ordenación y filtrado de recursos.
**Objetivo:** Asegurarse de que la API puede ordenar y filtrar correctamente los recursos de acuerdo con los parámetros proporcionados, mejorando la flexibilidad en las consultas de datos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso?sort=nombre&filter=activo:true`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Sorting and filtering handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 88. Verificar que la API maneja correctamente la búsqueda de recursos basada en criterios específicos.
**Objetivo:** Validar que la API permite búsquedas detalladas y específicas basadas en criterios proporcionados por el cliente, devolviendo los resultados adecuados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso?buscar=nombre:John`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Search based on criteria handled correctly", function () {
    pm.response.to.have.status(200);
    pm.expect(pm.response.json()).to.have.property("nombre", "John");
});
```

## 89. Verificar que la API maneja correctamente las solicitudes en lote y devuelve los recursos correctos para cada lote.
**Objetivo:** Asegurarse de que la API puede procesar correctamente solicitudes en lote, manejando múltiples operaciones en una única solicitud de manera eficiente.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/lote`
- Body: 
```javascript
[
    {"campo1": "valor1"},
    {"campo2": "valor2"}
]
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Batch requests handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 90. Verificar que la API maneja correctamente los webhooks y entrega los eventos correctos a los clientes suscritos.
**Objetivo:** Validar que la API puede gestionar webhooks correctamente, enviando los eventos adecuados a los clientes suscritos en tiempo real.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/webhook`
- Body: 
```javascript
{
    "evento": "creado",
    "recurso": "usuario"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Webhooks handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 91. Verificar que la API maneja correctamente la validación del lado del servidor y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API valida adecuadamente las entradas en el lado del servidor, protegiendo contra datos no válidos o maliciosos antes de procesarlos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "valor inválido"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Server-side validation handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 92. Verificar que la API maneja correctamente la validación del lado del cliente y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API requiere y respeta la validación del lado del cliente, asegurando que los datos enviados por el cliente cumplen con las reglas definidas.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "valor inválido"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Client-side validation handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 93. Verificar que la API maneja correctamente la validación a nivel de campo y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API realiza validaciones precisas a nivel de campo, rechazando entradas que no cumplan con los requisitos definidos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": ""
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Field-level validation handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 94. Verificar que la API maneja correctamente las transacciones de base de datos y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API puede manejar correctamente transacciones de base de datos, asegurando que las operaciones se realizan de manera consistente y confiable.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/transaccion`
- Body: 
```javascript
{
    "operacion": "insertar",
    "datos": {"campo": "valor"}
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Database transaction handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 95. Verificar que la API maneja correctamente las copias de seguridad y restauración de bases de datos y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API puede gestionar correctamente operaciones de copia de seguridad y restauración de bases de datos, protegiendo los datos críticos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/backup`
- Body: 
```javascript
{
    "accion": "backup"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Database backup handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 96. Verificar que la API maneja correctamente la encriptación y desencriptación de datos.
**Objetivo:** Validar que la API puede encriptar y desencriptar datos de manera segura, protegiendo la confidencialidad e integridad de la información.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/encriptar`
- Body: 
```javascript
{
    "datos": "texto claro"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Data encryption handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 97. Verificar que la API maneja correctamente la compresión y descompresión de datos.
**Objetivo:** Asegurarse de que la API puede comprimir y descomprimir datos de manera eficiente, reduciendo el tamaño de la carga útil y mejorando la transmisión de datos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/comprimir`
- Body: 
```javascript
{
    "datos": "texto a comprimir"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Data compression handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 98. Verificar que la API maneja correctamente la limitación de solicitudes basadas en la cuenta de usuario o dirección IP.
**Objetivo:** Validar que la API implementa políticas de limitación de solicitudes basadas en la cuenta de usuario o IP, previniendo abusos y garantizando la equidad en el acceso.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar múltiples solicitudes rápidamente.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Rate limiting by user account/IP handled correctly", function () {
    pm.response.to.have.status(429);
});
```

## 99. Verificar que la API maneja correctamente la autenticación basada en la cuenta de usuario o clave de API.
**Objetivo:** Asegurarse de que la API autentica correctamente las solicitudes basadas en la cuenta de usuario o la clave de API, protegiendo el acceso a los recursos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/privado`
- Headers: `Authorization: Bearer <API_KEY>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("User account/API key authentication handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 100. Verificar que la API maneja correctamente la autorización basada en roles de usuario o permisos.
**Objetivo:** Validar que la API implementa correctamente la autorización basada en roles o permisos, asegurando que los usuarios solo puedan acceder a los recursos autorizados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/admin`
- Headers: `Authorization: Bearer <token>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Role/permission-based authorization handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 101. Verificar que la API maneja correctamente el intercambio de recursos de origen cruzado (CORS) y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API soporta correctamente las políticas CORS, permitiendo solicitudes legítimas de orígenes cruzados y protegiendo contra accesos no autorizados.
**Ejemplo en Postman:**
- Método: `OPTIONS`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Origin: https://otro-dominio.com`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("CORS handled correctly", function () {
    pm.response.to.have.status(200);
    pm.response.to.have.header("Access-Control-Allow-Origin", "https://otro-dominio.com");
});
```

## 102. Verificar que la API maneja correctamente la sanitización de entradas y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API protege contra inyecciones maliciosas, sanitizando adecuadamente las entradas antes de procesarlas.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "<script>alert('xss')</script>"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Input sanitization handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 103. Verificar que la API maneja correctamente la sanitización de salidas y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API produce salidas seguras, protegiendo contra la exposición de datos sensibles o la ejecución de scripts no deseados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Output sanitization handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 104. Verificar que la API maneja correctamente la prevención de inyección SQL y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API está protegida contra ataques de inyección SQL, asegurando que las entradas no controladas no puedan alterar las consultas de la base de datos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "' OR '1'='1"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("SQL injection prevention handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 105. Verificar que la API maneja correctamente la prevención de scripting entre sitios (XSS) y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API es segura contra ataques XSS al validar y sanitizar adecuadamente los datos de entrada.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "<script>alert('xss')</script>"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("XSS prevention handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 106. Verificar que la API maneja correctamente las transacciones de base de datos y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API puede manejar correctamente transacciones de base de datos, asegurando que las operaciones se realizan de manera consistente y confiable.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/transaccion`
- Body: 
```javascript
{
    "operacion": "insertar",
    "datos": {"campo": "valor"}
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Database transaction handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 107. Verificar que la API maneja correctamente las copias de seguridad y restauración de bases de datos y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API puede gestionar correctamente operaciones de copia de seguridad y restauración de bases de datos, protegiendo los datos críticos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/backup`
- Body: 
```javascript
{
    "accion": "backup"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Database backup handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 108. Verificar que la API maneja correctamente la encriptación y desencriptación de datos.
**Objetivo:** Validar que la API puede encriptar y desencriptar datos de manera segura, protegiendo la confidencialidad e integridad de la información.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/encriptar`
- Body: 
```javascript
{
    "datos": "texto claro"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Data encryption handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 109. Verificar que la API maneja correctamente la compresión y descompresión de datos.
**Objetivo:** Asegurarse de que la API puede comprimir y descomprimir datos de manera eficiente, reduciendo el tamaño de la carga útil y mejorando la transmisión de datos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso/comprimir`
- Body: 
```javascript
{
    "datos": "texto a comprimir"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Data compression handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 110. Verificar que la API maneja correctamente la limitación de solicitudes basadas en la cuenta de usuario o dirección IP.
**Objetivo:** Validar que la API implementa políticas de limitación de solicitudes basadas en la cuenta de usuario o IP, previniendo abusos y garantizando la equidad en el acceso.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar múltiples solicitudes rápidamente.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Rate limiting by user account/IP handled correctly", function () {
    pm.response.to.have.status(429);
});
```

## 111. Verificar que la API maneja correctamente la autenticación basada en la cuenta de usuario o clave de API.
**Objetivo:** Asegurarse de que la API autentica correctamente las solicitudes basadas en la cuenta de usuario o la clave de API, protegiendo el acceso a los recursos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/privado`
- Headers: `Authorization: Bearer <API_KEY>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("User account/API key authentication handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 112. Verificar que la API maneja correctamente la autorización basada en roles de usuario o permisos.
**Objetivo:** Validar que la API implementa correctamente la autorización basada en roles o permisos, asegurando que los usuarios solo puedan acceder a los recursos autorizados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/admin`
- Headers: `Authorization: Bearer <token>`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Role/permission-based authorization handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 113. Verificar que la API maneja correctamente el intercambio de recursos de origen cruzado (CORS) y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API soporta correctamente las políticas CORS, permitiendo solicitudes legítimas de orígenes cruzados y protegiendo contra accesos no autorizados.
**Ejemplo en Postman:**
- Método: `OPTIONS`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Origin: https://otro-dominio.com`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("CORS handled correctly", function () {
    pm.response.to.have.status(200);
    pm.response.to.have.header("Access-Control-Allow-Origin", "https://otro-dominio.com");
});
```

## 114. Verificar que la API maneja correctamente la sanitización de entradas y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API protege contra inyecciones maliciosas, sanitizando adecuadamente las entradas antes de procesarlas.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "<script>alert('xss')</script>"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Input sanitization handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 115. Verificar que la API maneja correctamente la sanitización de salidas y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API produce salidas seguras, protegiendo contra la exposición de datos sensibles o la ejecución de scripts no deseados.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Output sanitization handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 116. Verificar que la API maneja correctamente la prevención de inyección SQL y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API está protegida contra ataques de inyección SQL, asegurando que las entradas no controladas no puedan alterar las consultas de la base de datos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "' OR '1'='1"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("SQL injection prevention handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 117. Verificar que la API maneja correctamente la prevención de scripting entre sitios (XSS) y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API es segura contra ataques XSS al validar y sanitizar adecuadamente los datos de entrada.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "campo": "<script>alert('xss')</script>"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("XSS prevention handled correctly", function () {
    pm.response.to.have.status(400);
});
```

## 118. Verificar que la API maneja correctamente la prevención de falsificación de solicitud entre sitios (CSRF) y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API está protegida contra ataques de falsificación de solicitud entre sitios, asegurando que las solicitudes se realizan solo por usuarios legítimos.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `X-CSRF-Token: <token_incorrecto>`
- Body: 
```javascript
{
    "campo": "valor"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("CSRF prevention handled correctly", function () {
    pm.response.to.have.status(403);
});
```

## 119. Verificar que la API maneja correctamente los enlaces rotos y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API devuelve respuestas adecuadas y errores específicos cuando se intenta acceder a recursos inexistentes.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/no-existente`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Broken links handled correctly", function () {
    pm.response.to.have.status(404);
});
```

## 120. Verificar que la API maneja correctamente las solicitudes de preflight de CORS y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API maneja correctamente las solicitudes preflight de CORS, permitiendo la comunicación entre dominios cuando es seguro hacerlo.
**Ejemplo en Postman:**
- Método: `OPTIONS`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Origin: https://otro-dominio.com`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("CORS preflight requests handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 121. Verificar que la API maneja correctamente el soporte multilingüe y devuelve los recursos correctos para cada idioma.
**Objetivo:** Asegurarse de que la API soporta múltiples idiomas, proporcionando respuestas en el idioma solicitado por el cliente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Accept-Language: es`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-language support handled correctly", function () {
    pm.response.to.have.status(200);
    pm.response.to.have.header("Content-Language", "es");
});
```

## 122. Verificar que la API maneja correctamente el soporte multimoneda y devuelve los recursos correctos para cada moneda.
**Objetivo:** Validar que la API puede gestionar correctamente diferentes monedas, proporcionando respuestas y cálculos adecuados en la moneda solicitada.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/precio`
- Headers: `Currency: USD`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-currency support handled correctly", function () {
    pm.response.to.have.status(200);
    pm.response.to.have.header("Currency", "USD");
});
```

## 123. Verificar que la API maneja correctamente el soporte multi-zona horaria y devuelve los recursos correctos para cada zona horaria.
**Objetivo:** Asegurarse de que la API puede manejar diferentes zonas horarias, devolviendo datos consistentes y correctos según la zona solicitada.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/tiempo`
- Headers: `Time-Zone: America/New_York`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-timezone support handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 124. Verificar que la API maneja correctamente el soporte multi-localización y devuelve los recursos correctos para cada localidad.
**Objetivo:** Validar que la API puede proporcionar respuestas localizadas correctamente, ajustando el contenido según la localidad del cliente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Locale: en-US`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-locale support handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 125. Verificar que la API maneja correctamente el soporte multi-región y devuelve los recursos correctos para cada región.
**Objetivo:** Asegurarse de que la API puede gestionar adecuadamente las diferencias regionales, proporcionando datos y servicios específicos para cada región.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Region: EU`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-region support handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 126. Verificar que la API maneja correctamente el soporte multi-inquilino y devuelve los recursos correctos para cada inquilino.
**Objetivo:** Validar que la API soporta adecuadamente arquitecturas multi-inquilino, asegurando la separación y privacidad de los datos entre inquilinos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/tenant`
- Headers: `Tenant-ID: 12345`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-tenant support handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 127. Verificar que la API maneja correctamente el soporte multi-entorno y devuelve los recursos correctos para cada entorno.
**Objetivo:** Asegurarse de que la API puede operar en múltiples entornos (desarrollo, prueba, producción) y proporcionar respuestas adecuadas según el entorno solicitado.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Environment: production`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-environment support handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 128. Verificar que la API maneja correctamente el soporte multiplataforma y devuelve los recursos correctos para cada plataforma.
**Objetivo:** Validar que la API puede servir diferentes plataformas (iOS, Android, web), devolviendo contenido optimizado y adecuado para cada una.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso`
- Headers: `Platform: iOS`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Multi-platform support handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 129. Verificar que la API devuelve el tiempo de respuesta correcto para diferentes tipos de solicitudes (por ejemplo, GET, POST, PUT, DELETE).
**Objetivo:** Asegurarse de que la API responde dentro de tiempos aceptables para cada tipo de solicitud, garantizando un rendimiento adecuado y consistente.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Response time for GET request is within limits", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});
```

## 130. Verificar que la API maneja correctamente las cargas útiles grandes y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API puede manejar eficientemente cargas útiles grandes, sin afectar negativamente el rendimiento o la estabilidad del sistema.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "datos": "a".repeat(1000000)
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Large payload handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 131. Verificar que la API maneja correctamente las cargas útiles pequeñas y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API puede manejar correctamente cargas útiles pequeñas, procesando eficientemente las solicitudes sin errores.
**Ejemplo en Postman:**
- Método: `POST`
- URL: `https://api.ejemplo.com/recurso`
- Body: 
```javascript
{
    "datos": "test"
}
```
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Small payload handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 132. Verificar que la API maneja correctamente las solicitudes concurrentes y devuelve los recursos correctos para cada solicitud.
**Objetivo:** Validar que la API puede gestionar correctamente múltiples solicitudes simultáneas, respondiendo con los datos adecuados para cada petición.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/1`
- Realizar múltiples solicitudes simultáneamente.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Concurrent requests handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 133. Verificar que la API maneja correctamente las solicitudes lentas y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API puede manejar solicitudes que toman más tiempo de lo habitual, devolviendo respuestas correctas sin fallos.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/lento`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Slow request handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 134. Verificar que la API maneja correctamente el tráfico alto y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API puede manejar correctamente un volumen elevado de tráfico, asegurando la estabilidad y rendimiento bajo alta carga.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/alta-demanda`
- Realizar múltiples solicitudes en un corto período.
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("High traffic handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 135. Verificar que la API maneja correctamente el tráfico bajo y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API sigue funcionando correctamente bajo condiciones de tráfico bajo, sin degradación en la calidad del servicio.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/baja-demanda`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Low traffic handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 136. Verificar que la API maneja correctamente la recuperación de errores y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API puede recuperarse adecuadamente de errores, proporcionando una respuesta útil y permitiendo la continuación del servicio.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/error`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Error recovery handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 137. Verificar que la API maneja correctamente la conmutación por error y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API soporta adecuadamente la conmutación por error, manteniendo la disponibilidad del servicio incluso ante fallos del sistema.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/failover`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Failover handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 138. Verificar que la API maneja correctamente el balanceo de carga y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Validar que la API puede distribuir eficientemente las solicitudes entre múltiples servidores, asegurando una carga equilibrada y evitando sobrecargas en un solo servidor.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/balanceo-carga`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Load balancing handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 139. Verificar que la API maneja correctamente la agrupación de servidores y devuelve el código de estado HTTP correcto y el mensaje de error.
**Objetivo:** Asegurarse de que la API soporta la agrupación de servidores, permitiendo la escalabilidad horizontal y la redundancia de servicios.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/recurso/cluster`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Server clustering handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 140. Verificar que la API maneja correctamente la versionización y devuelve los recursos correctos para cada versión.
**Objetivo:** Validar que la API gestiona adecuadamente las versiones, permitiendo a los clientes acceder a versiones específicas de recursos sin interferencias.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/v1/recurso`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("Versioning handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 141. Verificar que la API maneja correctamente la documentación de la API y devuelve los recursos correctos para cada punto final de la API.
**Objetivo:** Asegurarse de que la API proporciona documentación clara y precisa, permitiendo a los desarrolladores entender y utilizar adecuadamente los diferentes puntos finales.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/docs`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("API documentation handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 142. Verificar que la API maneja correctamente los registros de cambios de la API y devuelve los recursos correctos para cada cambio en la API.
**Objetivo:** Validar que la API mantiene un historial claro de cambios, permitiendo a los usuarios conocer las actualizaciones y modificaciones realizadas.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/changelog`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("API change logs handled correctly", function () {
    pm.response.to.have.status(200);
});
```

## 143. Verificar que la API maneja correctamente las pruebas de API y devuelve los recursos correctos para cada prueba de API.
**Objetivo:** Asegurarse de que la API soporta pruebas internas y externas, permitiendo la validación continua de su funcionalidad y rendimiento.
**Ejemplo en Postman:**
- Método: `GET`
- URL: `https://api.ejemplo.com/tests`
- Validación: En la pestaña de "Tests", agregar el siguiente script:
```javascript
pm.test("API testing handled correctly", function () {
    pm.response.to.have.status(200);
});
```
