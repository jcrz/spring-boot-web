# APUNTES DE SPRING BOOT WEB

20/04/20

## Controlador

En el enfoque de Spring para construir sitios web, las solicitudes HTTP son manejadas por un 
controlador. @Controller es la anotación que identifica a un controlador.

```java
package com.example.servingwebcontent;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
@GetMapping("/app")
public class IndexController {

	@GetMapping({"/index", "/", "/home"})
	public String index(@RequestParam(name="texto", required=false, defaultValue="World") String texto, Model model) {
		model.addAttribute("nombre", texto);
		return "index";
	}

}
```
En el ejemplo anterior, la clase **IndexController** maneja las solicitudes GET a partir de una direccion raiz "/app" especificada en la anotación **@GetMapping**. 

EL método index evalúa un parametro ("texto") desde la URL de tipo String. El objeto **Model** se encargará de dejar el valor accesible desde la plantilla vista utilizando la llave "nombre". Finalmente, retorna la vista, que por defecto se encuentra dentro del directorio src/main/resources > templates, en este caso un archivo index.html.

## Vista

**Thymeleaf** se encarga de representar el lado del servidor en el HTML. Analiza el index.html y evalua expresiones **th:text** para presentar el valor del parámetro que se configuró en el controlador. 

```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Getting Started: Serving Web Content</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
    <p th:text="'Saludos, ' + ${nombre} + '!'" />
</body>
</html>
```



