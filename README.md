# Proyecto 1

## Index
-El modelo de luz __wrap__ y __phong__ incluyendo un color para este mismo

-Soporte para __mapa de texturas__ y de __normales__ además de controlar su intensidad

-__Efecto de horizonte__, contiene el color de la iluminación (albedo)

-Efecto __banded__ que utiliza un __ramp texture__ para darle forma procedural

### Contenido
Utilizando un modelos de luz llamado __wrap__, el cual se basa del Lambert; iniciando en el color blanco, para lograr este efecto se utilizara "#pragma surface surf _(nombre: en este nosotros lo nombramos como deseemos)"_, en este caso se le llamo Toon, se construirá el modelo de luz con: half4 LightingToon; nunca va a superar al 1 y tampoco va a llegar una sombra debajo de 0.

Dando un brillo _(reflejo de la luz)_ a nuestro shader se utilizara el efecto __phong__ además de darle un color personalizado, para poder conseguirlo, se calculara el lambert con la normal, con el fin de calcular una nueva dirección, utilizando la función de reflect la cual refleja un vector, los reflejos pueden cambiar de posición pero no la luz y para esto se utiliza el viewdir; el specularity sirve para superponerse al albedo, el gloss para ver el tamaño que abarcara; se utiliza el max para poder proporcionar un máximo. ___Falloff:__ La caída de la sombra y en que magnitud va a ser. Llega la luz se esparce hasta que se ve negro.
Se calcula por medio de la normal: Producto punto ---> dot, el producto punto entre la normal y la dirección de la luz ---> N dot L_

Añadiendo textura se utilizaran los __mapas de textura y de normales__ además de manejar la __intensidad__ de los mapas de normales, para poder guardar una textura es importante en el código márcalas como 2D; manejando la intensidad se colocara un rango de -5 a 5. Durante el código se utilizan samples2D para guardar la variable de nuestras texturas, se proporcionan coordenadas añadiéndoles el uv el cual se encarga de sacarle el color a la textura.

Efecto de horizonte llamado __rim__ le proporcionara un brillo en las orillas a nuestro modelo, el cual inicia des del centro y finaliza hasta las orillas, para lograr esto se necesita invertirlo; no puede ser mayor que 1 y tampoco puede ser menor  0, si esto llegara a pasar, se reiniciaría, volvería a empezar y eso no es lo que se busca. Para que quede perfectamente en la orilla, es necesario añadir la saturación, ya que nos ayudara para controlar el color.

Efecto __banded__ la luz que se reciba, para poder hacer el efecto se utilizaran stees, los cuales se dividen en /256, llamándolo lightband; entre menos líneas abarca más zonas el efecto, para dividirlo en más se utiliza lightbandadd que es igual a stees/2, calculándolo con fixed. _Floor _el cual sirve para redondear variables, con la finalidad de conseguir una línea perfecta. Pero para dar mejor efecto a este, se añadirá la ramp texture, en la cual tendremos que crear una imagen .png, que vaya desde colores oscuros a más claros para realizar la sombra de este mismo. Con la cual es necesario utilizar las iteraciones y por ello se utiliza el tex2D, para añadir textura.

Para lograr la combinación de esto, se realizar el siguiente múltiplo:
```HSLS
c.rgb = lot * (NdotL * s.Albedo + specularity) * _LightColor0.rgb * rampColor * atten * bandedLightModel * diff;
```

Para lograr este proyecto, se utilizó unity y Visual Studio Code.
