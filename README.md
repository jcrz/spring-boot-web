# APUNTES SPRING BOOT WEB

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
	public String index(@RequestParam(name="name", required=false, defaultValue="World") String name, Model model) {
		model.addAttribute("name", name);
		return "greeting";
	}

}
``
En el ejemplo anterior, la clase IndexController maneja las solicitudes GET a partir de una direccion raiz "/app" especificada en la 
anotación @GetMapping. 