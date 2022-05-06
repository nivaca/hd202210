# TEI y XML

1.  El TEI hace énfasis en aquello que es común a todo tipo de
    documento, ya sea representado físicamente en forma digital en disco
    o tarjeta de memoria, en forma impresa como libro o periódico, en
    forma escrita como manuscrito o códice, o en forma inscrita en
    piedra o tablilla de cera.

Esta continuidad facilita la migración del texto desde manifestaciones
más antiguas, como la impresión o el manuscrito, a otras más nuevas,
como el disco o la pantalla. Por lo tanto, la visión del TEI de lo que
el texto realmente *es* está condicionada en gran medida por lo que el
texto *ha sido* en el pasado, sin comprometer demasiado lo que el texto
puede llegar a ser en el futuro. Intenta tratar todos los tipos de
documentos digitales de la misma manera, tanto si han \"nacido
digitales\" como si no.

1.  En consecuencia, el marco conceptual del TEI proporciona una forma
    útil de pensar acerca de la naturaleza del texto: constituye una
    especie de enciclopedia de nociones textuales generalmente
    acordadas.

En esta breve guía intentaremos ejemplificar algunas de estas nociones,
para lo cual utilizaremos el vocabulario definido por el TEI en sus
\<title>Directrices\</title>.

1.  Actualmente, los documentos TEI en formato digital se expresan por
    medio de un lenguaje de codificación formal muy extendido llamado
    XML, el *lenguaje de marcado extensible*, publicado por primera vez
    por el World Wide Web Consortium (W3C) en 1998, cuyos orígenes se
    remontan a los sistemas de preparación de documentos de la década
    de 1980.

XML ofrece una forma sencilla de representar datos estructurados como un
flujo lineal de datos de caracteres, y de marcar partes particulares de
ese flujo con *etiquetas* para indicar su función estructural o su
semántica. Al haberse convertido XML en una tecnología tan generalizada,
existen muchas guías introductorias excelentes, por lo que daremos por
sentado que el lector tiene un conocimiento básico de conceptos clave
como *elemento*, *atributo*, *esquema* y *espacio de nombres*
(*namespace*), que a continuación se glosarán brevemente en aras de la
inteligibilidad. Las \<title>Directrices TEI\</title> incluyen una
[Introducción suave a
XML](https://tei-c.org/release/doc/tei-p5-doc/en/html/SG.html), que
puede serle útil a los novatos, aunque es posible encontrar muchos otros
tutoriales sobre el tema en internet.

1.  El siguiente es un ejemplo de un documento XML mínimo:

``` xml
<?xml version="1.0"?>
<doc xmlns="http://example.org/namespace">
  <p n="1">Este es un párrafo.</p>
  <p n="2">Este párrafo menciona a <placeName>Bristol</placeName>.</p>
</doc>
```

1.  La primera línea de un documento XML siempre adopta la forma
    mostrada anteriormente: un tipo especial de instrucción que indica
    que lo que sigue es un documento XML conforme a la versión del
    estándar XML indicada (en este caso, la versión 1.0).

Un documento XML consiste en una secuencia de caracteres legibles por
humanos, sin códigos especiales adicionales ni datos binarios. Los
caracteres \< y \> se utilizan para marcar el inicio y el final de las
etiquetas dentro de esta secuencia. Una etiqueta puede ser de inicio
(como \<gi>p\</gi>) o de fin (como \</p>). Una etiqueta siempre comienza
con un nombre (doc, p, placeName en el ejemplo anterior) y también puede
contener especificaciones de atributo (como n=\"1\"). El propósito de
una etiqueta de inicio es marcar el punto en la secuencia de caracteres
en el que comienza algún *elemento*, de un tipo indicado por el nombre
de la etiqueta, y el propósito de una etiqueta de fin es marcar dónde
termina ese elemento. El propósito de una especificación de atributo es
añadir alguna información extra sobre la aparición de un elemento además
de su nombre. En el ejemplo anterior tenemos un elemento llamado
\<gi>doc\</gi> que contiene dos elementos \<gi>p\</gi>. Los elementos
\<gi>p\</gi> tienen ambos un atributo @n que proporciona un número, y
ambos contienen texto plano. El segundo elemento \<gi>p\</gi> también
contiene un elemento llamado \<gi>placeName\</gi>.

1.  Se dice que un documento XML como este está *bien formado* si
    respeta la sintaxis ejemplificada aquí, con las etiquetas de inicio
    y fin presentes y correctamente anidadas.

Pero el estándar XML no dice nada en absoluto sobre cómo deben nombrarse
los elementos o los atributos (a diferencia, por ejemplo, del HTML, que
define un conjunto específico de etiquetas que deben utilizarse de una
manera determinada en todos los documentos), y mucho menos sobre lo que
significan sus nombres. Podemos suponer que los elementos \<gi>p\</gi>
de arriba marcan párrafos numerados, pero no hay nada en la
representación XML que justifique esa suposición: podrían marcar
igualmente páginas, o entradas de un glosario, o versos. Por lo tanto,
si encuentro otro documento que contenga elementos \<gi>p\</gi>, ¿cómo
sabré si tienen la misma función? La función del atributo @xmlns de
arriba es ayudar a resolver este problema, al proporcionar un valor por
defecto para lo que se denomina el *espacio de nombres* de todos los
elementos contenidos por el elemento \<gi>doc\</gi>.

1.  No es extraño encontrar elementos pertenecientes a muchos espacios
    de nombres en un mismo documento: por ejemplo, un documento que
    contenga notación musical, gráficos vectoriales y texto, todo ello
    representado en XML, podría utilizar etiquetas de tres espacios de
    nombres diferentes: uno para los elementos musicales, otro para los
    gráficos y otro para los textuales.

Un espacio de nombres es una forma de etiquetar un grupo de elementos:
en nuestro ejemplo, su uso deja claro que los elementos \<gi>p\</gi>
aquí son diferentes de cualquier elemento \<gi>p\</gi> definido por otro
espacio de nombres cualquiera.

1.  La razón por la que se introduce el etiquetado en un documento es a
    fin de marcarlo y organizarlo para su procesamiento automático.

Si los párrafos están claramente marcados, un software de maquetación
puede distribuirlos adecuadamente. Si los nombres de lugar están
claramente marcados, un programa puede escogerlos automáticamente para
hacer un índice geográfico. Pero esto solo puede hacerse de forma fiable
si tenemos algún control sobre cómo se introducen las etiquetas en el
documento y dónde aparecen. La tecnología XML proporciona este nivel
adicional de control mediante lo que se denomina un *esquema*: un tipo
de léxico y gramática combinados para los documentos XML válidos. Arriba
mencionamos que un documento XML se dice que está *bien formado* si
respeta las reglas sintácticas del estándar de XML. También se puede
decir, alternativamente, que un documento es *válido* si las etiquetas
que contiene se ajustan a un esquema.

1.  Un *esquema* especifica un conjunto de nombres de elementos, los
    nombres y tipos de datos de los atributos asociados a ellos, y las
    reglas sobre los contextos en los que pueden aparecer legalmente.

Un esquema para nuestro sencillo ejemplo anterior dirá que existen
elementos llamados \<gi>doc\</gi>, \<gi>p\</gi>, \<gi>placeName\</gi>,
etc. También puede especificar que los elementos \<gi>p\</gi> pueden
aparecer dentro de los elementos \<gi>doc\</gi>, que los
\<gi>placeName\</gi> pueden aparecer dentro de los \<gi>p\</gi>, que el
atributo @n debe tener un valor numérico, etc. Nótese, sin embargo, que
un esquema XML aún no tiene modo de especificar que la etiqueta
\<gi>placeName\</gi> indica el nombre de un lugar, ni tampoco qué
entendemos por \"un lugar\": esas restricciones semánticas adicionales
deben especificarse en otra parte, por ejemplo mediante documentación
como la que proporcionan las \<title>Directrices TEI\</title>/.

1.  El TEI dispone de nombres y definiciones para cientos de etiquetas,
    junto con reglas sobre cómo pueden combinarse.

Más exactamente, las \<title>Directrices TEI\</title> definen unos
quinientos o seiscientos ***conceptos*** diferentes, junto con
especificaciones detalladas para los elementos XML y las clases de
elementos que pueden utilizarse para representarlos. La mayoría de los
documentos TEI, si no todos, solo necesitan de una pequeña cantidad de
lo que se proporciona. Por lo tanto, es un poco engañoso pensar en el
TEI como un único esquema monolítico. Para facilitar la
interoperabilidad, todos los documentos TEI utilizan componentes
extraídos del mismo esquema gigantesco, pero la mayoría de los proyectos
TEI utilizan subconjuntos bastante pequeños del este, y un proyecto bien
organizado generalmente tendrá su propia documentación personalizada que
identifique ese subconjunto.

1.  Uno puede utilizar software como la aplicación web
    [Roma](http://www.tei-c.org/Roma/) para elegir entre las
    especificaciones TEI y generar a partir de ellas un esquema adecuado
    a las necesidades de su propio proyecto. Alternativamente, uno puede
    simplemente diseñar un esquema a mano.

Trataremos este asunto con más detalle en un capítulo posterior. Las
*Directrices del TEI*, a las que se puede acceder gratuitamente desde el
sitio web <https://tei-c.org/Guidelines/>, constituyen un completo
manual de referencia para estos conceptos, que combina la especificación
técnica con una discusión detallada de cómo deben utilizarse.

1.  Hay una gran variedad de herramientas de software para crear,
    transformar y procesar documentos XML en general, o TEI-XML en
    particular.

Este es un asunto muy amplio y en rápida evolución que no trataremos
aquí, aunque es posible encontrar algunas indicaciones útiles en el
[sitio web del TEI](https://tei-c.org/) y en la [Wiki del
TEI](https://wiki.tei-c.org/index.php/Category%3ATools).

%%% Local Variables: %%% mode: org %%% ispell-local-dictionary:
\"spanish\" %%% End:
