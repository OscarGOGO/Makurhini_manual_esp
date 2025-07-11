# Consultas al CAT usando zacatuche y R

[](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/Zacatuche.png){width="591"}

## Cargar paquetes o instalarlos


```r
list.of.packages <- c("stars", "sf", "raster", "terra", "rmapshaper", "purrr",
                      "progress", "magrittr", "ghql", "dplyr", 
                      "parallel", "jsonlite", "future", "furrr")

new.packages <- list.of.packages[!(list.of.packages %in% installed.packages()[,"Package"])]
if(length(new.packages)) install.packages(new.packages, dependencies = TRUE)
purrr::walk(list.of.packages, function(x){suppressPackageStartupMessages(library(x, character.only = TRUE,
                                                                                 warn.conflicts = FALSE,  quietly = TRUE))})
```

## Cargar funciones usando un environment


```r
load("L:/BiodiversidadES/01_Conocimiento/01_Diversidad_biologica/04_Funciones/CAT_SNIB_env.RData") 
```


## Funciones generales

### *CatalogoClass()*


```r
CAT_SNIB_ENVI$CatalogoClass(grupo_verificado = NULL,
                            tabla = NULL,
                            taxon = NULL,
                            reino = NULL,
                            categoria_taxonomica = NULL,
                            categoria_busqueda = NULL,
                            multiple_lista = FALSE)
```

La función ayuda a construir los parámetros de consulta al zacatuche de forma fácil y ordenada. Si alguno de los parámetros necesarios para la consulta es incorrecto o falta, entonces mostrará un mensaje de error. Está función es usada para consultar al CAT y al SNIB ejemplares por lo que es muy importante conocer su funcionamiento y estructura.

#### **Parámetros**

-   **grupo_verificado** = *character*. Grupos taxonómicos definidos con la ayuda de la SCAT de la CONABIO. Se puede elegir una de las cuatro propuestas para agrupar los táxones: "grupo1", "grupo2", "grupo3" o taxon y "grupo4" o reino, o seleccionar uno o varios de los táxones que se encuentran en Grupos_consulta, por ejemplo: "Hongos" o algo más especifico como "Ascomycota".

La tabla de grupos taxonómicos puede consultarse de la siguiente forma:


```r
CAT_SNIB_ENVI$Grupos_consulta
```


```{=html}
<div class="datatables html-widget html-fill-item-overflow-hidden html-fill-item" id="htmlwidget-b36ec5dda9cbf920feee" style="width:100%;height:auto;"></div>
<script type="application/json" data-for="htmlwidget-b36ec5dda9cbf920feee">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54","55","56","57","58","59","60","61","62","63","64","65","66","67","68","69","70","71","72","73","74","75","76","77","78","79","80","81","82","83","84","85","86","87","88","89","90","91","92","93","94","95","96","97","98","99","100","101","102","103","104","105","106","107","108","109","110","111","112","113","114","115","116","117","118","119","120","121","122","123","124","125","126","127","128","129","130","131","132","133","134","135","136","137","138","139","140","141","142","143","144","145","146","147","148","149","150","151","152","153","154","155","156","157","158","159","160","161","162","163","164","165","166","167","168","169","170","171","172","173","174","175","176","177","178","179","180","181","182","183","184","185","186","187","188","189"],["bacterias","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","hongos","hongos","hongos","hongos","hongos","hongos","plantas no vasculares","plantas no vasculares","plantas no vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","invertebrados no artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","artropodos","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","vertebrados","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares","plantas vasculares"],["cyanobacterias","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","algas","hongos","hongos","hongos","hongos","hongos","hongos","briofitas","antoceros","hepaticas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","pteridofitas","gimnospermas","gimnospermas","gimnospermas","gimnospermas","gimnospermas","gimnospermas","gimnospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas","esponjas de mar","esponjas de mar","esponjas de mar","esponjas de mar","placozoa","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","cnidarios","ctenoforos","chaetognatha","platelmintos","moluscos","moluscos","moluscos","moluscos","moluscos","gusanos anelidos","gusanos anelidos","gusanos anelidos","sipuncula","rotifera","acanthocephala","foronideos","briozoos","brachiopodos","tardigrados","onychophora","equinodermos","urocordados","urocordados","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","crustaceos","quelicerados","quelicerados","quelicerados","miriapodos","miriapodos","miriapodos","miriapodos","hexapodos","hexapodos","hexapodos","hexapodos","peces","peces","peces","peces","peces","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","mamiferos","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","aves","anfibios","anfibios","anfibios","reptiles","reptiles","reptiles","gimnospermas","pteridofitas","angiospermas","angiospermas","angiospermas","angiospermas","angiospermas"],["Cyanobacteria","Bacillariophyta","Cryptophyta","Choanozoa","Dinophyta","Euglenozoa","Haptophyta","Charophyta","Chlorophyta","Rhodophyta","Chrysophyceae","Phaeophyceae","Bolidophyceae","Dictyochophyceae","Picophagophyceae","Raphidophyceae","Synurales","Xanthophyceae","Ascomycota","Basidiomycota","Chytridiomycota","Glomeromycota","Zygomycota","Entomophthorales","Bryophyta","Anthocerotophyta","Marchantiophyta","Lycopodiales","Isoetales","Selaginellales","Equisetales","Ophioglossales","Marattiaceae","Osmundales","Hymenophyllales","Gleicheniales","Schizaeales","Salviniales","Cyatheales","Polypodiales","Pinaceae","Cupressaceae","Podocarpaceae","Cycadaceae","Zamiaceae","Ephedraceae","Ginkgoaceae","Asteraceae","Cactaceae","Crassulaceae","Euphorbiaceae","Fabaceae","Fagaceae","Lamiaceae","Rubiaceae","Solanaceae","Orchidaceae","Asparagaceae","Arecaceae","Bromeliaceae","Poaceae","Calcarea","Demospongiae","Hexactinellida","Homoscleromorpha","Placozoa","Spirularia","Penicillaria","Actiniaria","Zoantharia","Alcyonacea","Pennatulacea","Antipatharia","Corallimorpharia","Scleractinia","Cubozoa","Hydrozoa","Scyphozoa","Ctenophora","Chaetognatha","Platyhelminthes","Bivalvia","Cephalopoda","Gastropoda","Polyplacophora","Scaphopoda","Polychaeta","Lumbricidae","Arhynchobdellida","Sipuncula","Rotifera","Acanthocephala","Phoronida","Bryozoa","Brachiopoda","Tardigrada","Onychophora","Echinodermata","Ascidiacea","Thaliacea","Anostraca","Diplostraca","Laevicaudata","Notostraca","Remipedia","Cephalocarida","Maxillopoda","Ostracoda","Stomatopoda","Amphipoda","Cumacea","Isopoda","Lophogastrida","Tanaidacea","Thermosbaenacea","Euphausiacea","Leptostraca","Decapoda","Mysida","Arachnida","Xiphosura","Pycnogonida","Chilopoda","Diplopoda","Pauropoda","Symphyla","Insecta","Diplura","Collembola","Protura","Myxini","Leptocardii","Chondrichthyes","Osteichthyes","Petromyzontida","Rodentia","Chiroptera","Carnivora","Soricomorpha","Cetacea","Artiodactyla","Lagomorpha","Didelphimorphia","Primates","Pilosa","Perissodactyla","Cingulata","Sirenia","Passeriformes","Charadriiformes","Apodiformes","Anseriformes","Accipitriformes","Procellariiformes","Piciformes","Strigiformes","Columbiformes","Galliformes","Psittaciformes","Pelecaniformes","Gruiformes","Falconiformes","Caprimulgiformes","Suliformes","Cuculiformes","Coraciiformes","Trogoniformes","Podicipediformes","Gaviiformes","Cathartiformes","Tinamiformes","Phaethontiformes","Nyctibiiformes","Ciconiiformes","Phoenicopteriformes","Eurypygiformes","Anura","Caudata","Gymnophiona","Crocodylia","Squamata","Testudines","Taxaceae","Psilotales","Commelinaceae","Rosaceae","Burseraceae","Apocynaceae","Campanulaceae"],["Prokaryotae","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Protoctista","Fungi","Fungi","Fungi","Fungi","Fungi","Fungi","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Animalia","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae","Plantae"],["división","división","división","división","división","phylum","división","división","división","división","clase","clase","clase","clase","clase","clase","orden","clase","división","división","división","división","división","orden","división","división","división","orden","orden","orden","orden","orden","familia","orden","orden","orden","orden","orden","orden","orden","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","familia","clase","clase","clase","clase","phylum","orden","orden","orden","orden","orden","orden","orden","orden","orden","clase","clase","clase","phylum","phylum","phylum","clase","clase","clase","clase","clase","clase","familia","orden","phylum","phylum","phylum","phylum","phylum","phylum","phylum","phylum","phylum","clase","clase","orden","orden","orden","orden","clase","clase","clase","clase","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","clase","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","orden","familia","orden","familia","familia","familia","familia","familia"],["especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","clase","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie","especie"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>grupo1<\/th>\n      <th>grupo2<\/th>\n      <th>taxon<\/th>\n      <th>reino<\/th>\n      <th>categoria_taxonomica<\/th>\n      <th>categoria_busqueda<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"order":[],"autoWidth":false,"orderClasses":false,"columnDefs":[{"orderable":false,"targets":0}]}},"evals":[],"jsHooks":[]}</script>
```

-   **tabla** = *`data.frame`*. Una tabla con cuatro columnas, dos obligatorias: `Taxon` = Taxón que se consulta en el CAT; `Reino` = Reino al que pertenece el taxón que se consulta. Y dos opcionales: `Categoría taxonómica` = Categoría taxonómica del taxón que se consulta (e.g., subespecie, especie, género, familia, clase, suborden, orden); `Categoría del taxon de búsqueda` = Por default se entiende que se busca información a nivel de especie (e.g., especies del taxón que se consulta), pero en esta columna se puede especificar si la información que se consulta se requiere a otro nivel (e.g., colocar la palabra 'género' te devolverá información sobre los géneros del taxón que se consulta). [*El nombre de las columnas no es importante, el orden sí.*]{.underline}

-   **taxon** = *`character`*. Si solo consultas información de un grupo taxonómico puedes colocar su nombre aquí y deberás usar los tres parámetros siguientes, dos de ellos opcionales.

-   **reino** = *`character`*. Indica el reino al que pertenece el taxón que se busca.

-   **categoria_taxonomica** = *`character`*. Opcional, indica la categoría taxonómica del taxón que se busca, por ejemplo, subespecie, especie, género, familia, clase, suborden u orden, es decir, si mi taxon es '*Panthera onca*' puedo especificar en esta columna que se trata de una 'especie'.

-   **categoria_busqueda** = *`character`*. Opcional, indica la categoría taxonómica del taxón que se busca, por ejemplo, subespecie, especie, género, familia, clase, suborden u orden, es decir, si se coloca 'género' te devolverá información sobre los géneros del taxón que se consulta.

#### Ejemplos

1.  Usando una tabla que previamente se pudo cargar con `read.csv`, `read.table`, `read_csv` u otras funciones. Las columnas de la table deben mantener el mismo orden que la tabla de abajo, es decir, taxón, reino, categoría taxonómica, categoría de búsqueda.

En el ejemplo se busca información a nivel de **especie** para el orden **Carnivora** que pertenece al reino **Animalia** y de la familia **Fagaceae** que pertenece al reino **Plantae**


```r
tabla_consulta <- data.frame(taxon = c("Carnivora", "Fagaceae"),
                             reino = c("Animalia", "Plantae"),
                             categoria_taxonomica = c("orden", "familia"),
                             categoria_busqueda = c("especie", "especie"))
tabla_consulta 
#>       taxon    reino categoria_taxonomica
#> 1 Carnivora Animalia                orden
#> 2  Fagaceae  Plantae              familia
#>   categoria_busqueda
#> 1            especie
#> 2            especie
```


```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(tabla = tabla_consulta)
entrada_consulta
#> [[1]]
#> An object of class "Catalogo"
#> Slot "taxa":
#> [1] "Carnivora AND taxonRank:especie"
#> 
#> Slot "kingdom":
#> [1] "Animalia"
#> 
#> Slot "category":
#> [1] "orden"
#> 
#> Slot "gverif":
#> [1] ""
#> 
#> 
#> [[2]]
#> An object of class "Catalogo"
#> Slot "taxa":
#> [1] "Fagaceae AND taxonRank:especie"
#> 
#> Slot "kingdom":
#> [1] "Plantae"
#> 
#> Slot "category":
#> [1] "familia"
#> 
#> Slot "gverif":
#> [1] ""
```

2.  Usando alguno de los grupos que se encuentran en la tabla **Grupos_consulta** (ver parámetros) y que ya fueron verificados por el SCAT


```r
#Alguno de los grupos que ya fueron verificados
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(grupo_verificado = "Vertebrados")

entrada_consulta[[10]]
#> An object of class "Catalogo"
#> Slot "taxa":
#> [1] "/Cetacea/ AND taxonRank:especie"
#> 
#> Slot "kingdom":
#> [1] "Animalia"
#> 
#> Slot "category":
#> [1] "orden"
#> 
#> Slot "gverif":
#> [1] "Vertebrados"
```

3.  Buscando un solo taxón o grupo taxonómico. En los ejemplos primero se consultan las especies del orden Carnívora y después la información de la especie *Tapirus bairdii*.


```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = "Carnivora", 
                                                reino = "Animalia",
                                                categoria_taxonomica = "orden",
                                                categoria_busqueda = "especie")
entrada_consulta
#> [[1]]
#> An object of class "Catalogo"
#> Slot "taxa":
#> [1] "/Carnivora/ AND taxonRank:especie"
#> 
#> Slot "kingdom":
#> [1] "Animalia"
#> 
#> Slot "category":
#> [1] "orden"
#> 
#> Slot "gverif":
#> [1] ""
```


```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = "Tapirus bairdii",
                                                reino = "Animalia",
                                                categoria_taxonomica = "especie", categoria_busqueda = "especie")
entrada_consulta
#> [[1]]
#> An object of class "Catalogo"
#> Slot "taxa":
#> [1] "/Tapirus bairdii/ AND taxonRank:especie"
#> 
#> Slot "kingdom":
#> [1] "Animalia"
#> 
#> Slot "category":
#> [1] "especie"
#> 
#> Slot "gverif":
#> [1] ""
```


## Funciones para consultar al CAT del SNIB

La función principal es **`taxon_CAT`** y realiza la consulta al zacatuche y aplica filtros para descartar especies exóticas e invasoras, duplicados, o identificadores con NA. Estos filtros son opcionales. Los parámetros son:

-   **consulta_CAT**. *`Clase consulta`*, puede ser una lista de consultas. Ver [CatalogoClass()]

-   **remover_exotica_invasora**. *`logical`*`, default = TRUE`. Remover (TRUE) especies exóticas e invasoras de la tabla final.

-   **solo_nativas_endemicas**. *`logical`*`, default = FALSE`. Quedarte solo con las especies marcadas como nativas y endémicas (TRUE). Se tiene el riesgo de quitar especies que no han sido evaluadas y cuyo campo aparece como vacío, es decir, `""`.

-   **remover_duplicados**. *`logical`*`, default = TRUE`. Remover (TRUE) ids validos duplicados.

-   **intern**. *`logical`*`, default = TRUE`. Observar el progreso de la consulta.

-   **parallel**. *`numeric`*`, default = NULL`. Si se quiere paralelizar entonces se debe proporcionar el número de núcleos con los que se quiere trabajar. Queda a criterio del usuario para no saturar la máquina.

La función depende de las siguientes funciones:

1.  `Consulta_searchTaxon`: genera una consulta y un cliente (conexión a graphql) para zacatuche.

2.  `met_1`**:** hace la consulta a zacatuche GraphQL. Es apropiada para consultas que devuelvan menos de 9,000 registros del CAT.

3.  `met_2`**:** hace la consulta a zacatuche GraphQL. Es apropiada para consultas que devuelvan más de 9,000 registros del CAT. Se usa un loop de tipo `repeat{}` y en cada iteracción se descarga un maximo de 8,000 registros para no saturar a Zacatuche graphQL. El repeat puede ser paralelizado.

4.  `busqueda_CAT`: corre la función `Consulta_serachTaxon` para conectarse a zacatuche y consultar al CAT del SNIB y para eso corre las funciones `met_1` y `met_2`. Si son varias consultas entonces usa un `lapply()` o paraleliza el proceso usando `future_map()` de la librería `furrr`.

5.  `tabla_CAT`**:** Arregla y estructura los datos en un data.frame. La salida de la consulta realizada al zacatuche es primero json y después una lista, la función tabla_CAT transforma la lista y sublistas en un data.frame y filtra la información para eliminar registros con campos vacíos, sin id, que pertenecen a un Reino distinto al consultado, etc.

![**Flujo de trabajo de la función taxon_CAT()**](C:/Users/ogodinez/Documents/CnM/PruebaLibro/Libro_Prueba1/images/CAT_1.png){width="591"}

#### Ejemplos

**1.**  Usando una tabla que previamente se pudo cargar con `read.csv`, `read.table`, `read_csv` u otras funciones. Las columnas de la table deben mantener el mismo orden que la tabla de abajo, es decir, taxón, reino, categoría taxonómica, categoría de búsqueda.

En el ejemplo se busca información a nivel de **especie** para el orden **Carnivora** que pertenece al reino **Animalia** y de la familia **Fagaceae** que pertenece al reino **Plantae**


```r
tabla_consulta <- data.frame(taxon = c("Carnivora", "Fagaceae"),
                             reino = c("Animalia", "Plantae"),
                             categoria_taxonomica = c("orden", "familia"),
                             categoria_busqueda = c("especie", "especie"))
tabla_consulta
#>       taxon    reino categoria_taxonomica
#> 1 Carnivora Animalia                orden
#> 2  Fagaceae  Plantae              familia
#>   categoria_busqueda
#> 1            especie
#> 2            especie
```

```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(tabla = tabla_consulta)

resultado_consulta <- CAT_SNIB_ENVI$taxon_CAT(consulta_CAT = entrada_consulta,
                                              remover_exotica_invasora = TRUE,
                                              remover_duplicados = TRUE, intern = FALSE)
```


Ver resultado:


```r
resultado_consulta
```




**2.**  Usando alguno de los grupos que se encuentran en la tabla **Grupos_consulta** (ver parámetros) y que ya fueron verificados por el SCAT


```r
#Alguno de los grupos que ya fueron verificados
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(grupo_verificado = "Anfibios")

resultado_consulta <- CAT_SNIB_ENVI$taxon_CAT(consulta_CAT = entrada_consulta,
                                              remover_exotica_invasora = TRUE,
                                              remover_duplicados = TRUE, intern = FALSE)
```

Ver resultado:


```r
resultado_consulta
```




**3.**  Buscando un solo taxón o grupo taxonómico. En los ejemplos primero se consultan las especies del orden Carnívora y después la información de la especie *Tapirus bairdii*.


```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = "Carnivora", 
                                                reino = "Animalia",
                                                categoria_taxonomica = "orden",
                                                categoria_busqueda = "especie")

Carnivoros <- CAT_SNIB_ENVI$taxon_CAT(consulta_CAT = entrada_consulta, 
                                      remover_exotica_invasora = TRUE, 
                                      remover_duplicados = TRUE)
Carnivoros
```




```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = "Tapirus bairdii", reino = "Animalia", categoria_taxonomica = "especie", categoria_busqueda = "especie")

tapir <- CAT_SNIB_ENVI$taxon_CAT(consulta_CAT = entrada_consulta, 
                                 remover_exotica_invasora = TRUE, 
                                 remover_duplicados = TRUE)
tapir
```


# Consulta de SNIB registros usando zacatuche y R


## Usando ID valido

Aquí el parámetro buscar_CAT puede ser igual a FALSE, es decir no hace falta consultar al CAT para obtener los id validos porque previamente los obtuve


```r
 Tapir <- tryCatch(CAT_SNIB_ENVI$taxon_coordenadas(consulta_SNIB = tapir$Valido.id,
                                                            remover_exotica_invasora = TRUE,
                                                            remover_duplicados = TRUE,
                                                            filtros = list(pais = "MEXICO", 
                                                                           anio_min = NULL, 
                                                                           anio_max = NULL,
                                                                           rem_novalPais = TRUE,
                                                                           rem_novalEdo = TRUE,
                                                                           rem_novalMun = FALSE,
                                                                           rem_novalLoc = FALSE),
                                                            parallel = 4,
                                                            intern = FALSE,
                                                            messages = FALSE,
                                                            tabla_TipoDistribucion = TRUE,
                                                            returnCAT = FALSE, 
                                                            buscar_CAT = FALSE,
                                                            save_RDS = NULL), error = function(err)err)
```


## Usando Nombre cientifico

Con esta opción tenemos que dar el valor de TRUE al parámetro *buscar_cat* para que busqué el id valido.


```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = "Tapirus bairdii", reino = "Animalia", categoria_taxonomica = "especie", categoria_busqueda = "especie")

 Tapir.2 <- tryCatch(CAT_SNIB_ENVI$taxon_coordenadas(consulta_SNIB = entrada_consulta,
                                                            remover_exotica_invasora = TRUE,
                                                            remover_duplicados = TRUE,
                                                            filtros = list(pais = "MEXICO", 
                                                                           anio_min = NULL, 
                                                                           anio_max = NULL,
                                                                           rem_novalPais = TRUE,
                                                                           rem_novalEdo = TRUE,
                                                                           rem_novalMun = FALSE,
                                                                           rem_novalLoc = FALSE),
                                                            parallel = NULL,
                                                            intern = FALSE,
                                                            messages = FALSE,
                                                            tabla_TipoDistribucion = TRUE,
                                                            returnCAT = FALSE, 
                                                            buscar_CAT = TRUE,
                                                            save_RDS = NULL), error = function(err)err)
```





## Podemos buscar varias especies


```r
entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = c("Tapirus bairdii", "Manilkara zapota"), 
                                                reino = c("Animalia", "Plantae"),
                                                categoria_taxonomica = "especie",
                                                categoria_busqueda = "especie")

 varios <- tryCatch(CAT_SNIB_ENVI$taxon_coordenadas(consulta_SNIB = entrada_consulta,
                                                            remover_exotica_invasora = TRUE,
                                                            remover_duplicados = TRUE,
                                                            terrestres = TRUE,
                                                            dulceacuicola = TRUE,
                                                            marinas = FALSE,
                                                            filtros = list(pais = "MEXICO", 
                                                                           anio_min = NULL, 
                                                                           anio_max = NULL,
                                                                           rem_novalPais = TRUE,
                                                                           rem_novalEdo = TRUE,
                                                                           rem_novalMun = FALSE,
                                                                           rem_novalLoc = FALSE),
                                                            parallel = NULL,
                                                            intern = FALSE,
                                                            messages = FALSE,
                                                            tabla_TipoDistribucion = TRUE,
                                                            returnCAT = FALSE, 
                                                            buscar_CAT = TRUE,
                                                            save_RDS = NULL), error = function(err)err)

```


## Podemos alterar la busqueda 


```r
Ejemplares_query <- CAT_SNIB_ENVI$Consulta_searchEjemplar(DATOS_URL = "http://zacatuche2.conabio.gob.mx:4000/graphql",
                                                          idnombrecat = c("id", "taxon"),
                                                          taxonValido = c("id", "taxon"),
                                                          ejemplar = c("latitud", "longitud", "aniocolecta", "validacionambiente",
                                                                       "geovalidacion", "exoticainvasora", "nivelprioridad",
                                                                       "nom059", "iucn", "cites", "endemismo",
                                                                       "paiscoleccion", "paismapa",
                                                                       "especie", "especievalida",
                                                                       "grupobio"))

entrada_consulta <- CAT_SNIB_ENVI$CatalogoClass(taxon = c("Tapirus bairdii", "Manilkara zapota"), 
                                                reino = c("Animalia", "Plantae"),
                                                categoria_taxonomica = "especie",
                                                categoria_busqueda = "especie")

 varios <- tryCatch(CAT_SNIB_ENVI$taxon_coordenadas(consulta_SNIB = entrada_consulta,
                                                            remover_exotica_invasora = TRUE,
                                                            remover_duplicados = TRUE,
                                                            filtros = list(pais = "MEXICO", 
                                                                           anio_min = NULL, 
                                                                           anio_max = NULL,
                                                                           rem_novalPais = TRUE,
                                                                           rem_novalEdo = TRUE,
                                                                           rem_novalMun = FALSE,
                                                                           rem_novalLoc = FALSE),
                                                            parallel = NULL,
                                                            intern = FALSE,
                                                            messages = FALSE,
                                                            Ejemplares_query = Ejemplares_query,
                                                            tabla_TipoDistribucion = TRUE,
                                                            returnCAT = FALSE, 
                                                            buscar_CAT = TRUE,
                                                            save_RDS = NULL), error = function(err)err)
```



