# 📊Proyecto Power BI – Análisis de Tienda de Música en Línea📊

## descripción:
Este proyecto de análisis fue realizado sobre una tienda de música digital. Utiliza Power BI para generar visualizaciones interactivas a partir de datos estructurados en SQL Server. 
El objetivo es brindar insights valiosos sobre el comportamiento de clientes, tendencias de ventas, desempeño de artistas y álbumes más populares.

---

## Tecnologías utilizadas

- Power BI Desktop
- SQL Server
- DAX (Data Analysis Expressions)
- Git & GitHub
- Visual Studio Code

---

## Objetivo del análisis

Explorar y visualizar datos históricos de ventas para:

- Identificar a los clientes más valiosos
- Evaluar el desempeño por artista, álbum y género
- Visualizar las ventas por país y por año
- Medir KPIs clave del negocio

---

## Capturas del Dashboard

### Inicio – Presentación

![Inicio](https://github.com/user-attachments/assets/5a7eb66f-a53d-47b8-b0d7-1b0e62939403)

### Análisis General

![Analisis Geeneral](https://github.com/user-attachments/assets/7423aae4-845e-46da-8228-1a8dcb878edf)

### Top Clientes y Álbumes

![Top Clientes y Albunes](https://github.com/user-attachments/assets/af22904b-54f3-4d09-abdb-6dad22ed5ba7)


### Análisis por Artista

![Analsis Artistas](https://github.com/user-attachments/assets/7bedf414-d545-4a4d-82a5-605fe426c1e3)


### KPIs del Negocio

![KPIs](https://github.com/user-attachments/assets/fd1103a4-2e2f-481c-8865-430943a100e7)

---

## Acceso en línea

Puedes ver el dashboard en línea a través de Power BI Public:

👉 *[Ver Dashboard Power BI](https://goo.su/Dw5aP)*  


---

## Estructura de la base de datos (Modelo Relacional)

![E-R](https://github.com/user-attachments/assets/153967eb-4b5f-444b-9436-49470ef674ea)


- La base de datos está normalizada y contiene tablas como:
  - customers, invoices, invoice_items, tracks
  - albums, artists, genres, employees, media_types
- Las relaciones clave permiten generar análisis multitabla en Power BI.

---

## Medidas DAX utilizadas

El proyecto utiliza más de 15 medidas DAX para cálculos como:
---
#### Módulo: Función  CALCULATE
---
Álbumes Distintos por Año = 
CALCULATE(DISTINCTCOUNT(Album[AlbumId]), RELATEDTABLE(Track), RELATEDTABLE(InvoiceLine), RELATEDTABLE(Invoice))

Artistas Distintos por Año2 = 

CALCULATE(
    DISTINCTCOUNT(Album[ArtistId]),
    ALLEXCEPT(Invoice, Invoice[AñoVenta]),
    RELATEDTABLE(Track)
)

Clientes Distintos por Año = 
CALCULATE(DISTINCTCOUNT(Customer[CustomerId]), RELATEDTABLE(Invoice))

CrecimientoVentasInteranual = 
VAR VentasActuales = SUM('InvoiceLine'[Total de Ventas])
VAR VentasAct = CALCULATE(
    SUM('InvoiceLine'[Total de Ventas]),
    DATEADD('Invoice'[InvoiceDate], -1, YEAR)
)
RETURN
    IF(
        ISBLANK(VentasAct) || VentasAct = 0,
        BLANK(),
        DIVIDE(VentasAct - VentasAct, VentasAct
    ))

Géneros Distintos por Año = 
CALCULATE(DISTINCTCOUNT(Genre[GenreId]), RELATEDTABLE(Track), RELATEDTABLE(InvoiceLine), RELATEDTABLE(Invoice))

---
Módulo: Funciones matemáticas y estadísticas

---
Ticket Promedio por Cliente = 
[Ventas Totales] / DISTINCTCOUNT('Customer'[CustomerId])

Ventas Anuales = 
CALCULATE(
    [Ventas Totales]
)

Ventas Totales = 
SUM(InvoiceLine[Total de Ventas]) 
---

Módulo: Función RELATED

---
Ventas por Artista = 
CALCULATE(
    SUM(InvoiceLine[Total de Ventas]),
    RELATEDTABLE(Track),
    RELATEDTABLE(Album)
)

---
Módulo: Función UMMARIZE

---


Top 5 Albunes = 
TOPN(5, SUMMARIZE('Album', 'Album'[AlbumId], "Total Venta", [Ventas Totales]), [Total Venta], DESC)

Top 5 Artistas = 
TOPN(5, SUMMARIZE('Artist', 'Artist'[ArtistId], "TotalVenta", [Ventas Totales]), [TotalVenta], DESC)


Top 5 Clientes = 
TOPN(5, SUMMARIZE('Customer', 'Customer'[CustomerId], "TotalVenta", [Ventas Totales]), [TotalVenta], DESC)

Top 5 Generos = 
TOPN(5, SUMMARIZE('Genre', 'Genre'[GenreId], "TotalVenta", [Ventas Totales]), [TotalVenta], DESC)

*Archivo con medidas:* (https://goo.su/o8Jlf)



---

## Autor

*Gustavo Mijahuanga López*  
*Analista de Datos* – GusData  
*Email:* gmijahuangalopez@gmail.com  
*GitHub:* [Gustavo123-hub](https://github.com/Gustavo123-hub)
*LinkedIn:* Gustavo Adolfo Mijahuanga Lopez (https://www.linkedin.com/in/g-m-l/)

---
