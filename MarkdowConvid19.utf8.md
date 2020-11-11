
<!-- rnb-text-begin -->

---
title: "Analisis Covid19"
output: html_notebook
---


<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeSh0aWR5dmVyc2UpXG5gYGAifQ== -->

```r
library(tidyverse)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiUmVnaXN0ZXJlZCBTMyBtZXRob2RzIG92ZXJ3cml0dGVuIGJ5ICdkYnBseXInOlxuICBtZXRob2QgICAgICAgICBmcm9tXG4gIHByaW50LnRibF9sYXp5ICAgICBcbiAgcHJpbnQudGJsX3NxbCAgICAgIFxuLS0gQXR0YWNoaW5nIHBhY2thZ2VzIC0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLSB0aWR5dmVyc2UgMS4zLjAgLS1cbnYgZ2dwbG90MiAzLjMuMCAgICAgdiBwdXJyciAgIDAuMy40XG52IHRpYmJsZSAgMy4wLjAgICAgIHYgZHBseXIgICAxLjAuMFxudiB0aWR5ciAgIDEuMC4yICAgICB2IHN0cmluZ3IgMS40LjBcbnYgcmVhZHIgICAxLjMuMSAgICAgdiBmb3JjYXRzIDAuNS4wXG4tLSBDb25mbGljdHMgLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tLS0tIHRpZHl2ZXJzZV9jb25mbGljdHMoKSAtLVxueCBkcGx5cjo6ZmlsdGVyKCkgbWFza3Mgc3RhdHM6OmZpbHRlcigpXG54IGRwbHlyOjpsYWcoKSAgICBtYXNrcyBzdGF0czo6bGFnKClcbiJ9 -->

```
Registered S3 methods overwritten by 'dbplyr':
  method         from
  print.tbl_lazy     
  print.tbl_sql      
-- Attaching packages --------------------------------------- tidyverse 1.3.0 --
v ggplot2 3.3.0     v purrr   0.3.4
v tibble  3.0.0     v dplyr   1.0.0
v tidyr   1.0.2     v stringr 1.4.0
v readr   1.3.1     v forcats 0.5.0
-- Conflicts ------------------------------------------ tidyverse_conflicts() --
x dplyr::filter() masks stats::filter()
x dplyr::lag()    masks stats::lag()
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeShTdXBlckxlYXJuZXIpXG5gYGAifQ== -->

```r
library(SuperLearner)
```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiTG9hZGluZyByZXF1aXJlZCBwYWNrYWdlOiBubmxzXG5TdXBlciBMZWFybmVyXG5WZXJzaW9uOiAyLjAtMjZcblBhY2thZ2UgY3JlYXRlZCBvbiAyMDE5LTEwLTI3XG4ifQ== -->

```
Loading required package: nnls
Super Learner
Version: 2.0-26
Package created on 2019-10-27
```



<!-- rnb-output-end -->

<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxubGlicmFyeSh4bHN4KVxubGlicmFyeShnZ3Bsb3QyKVxuXG5gYGAifQ== -->

```r
library(xlsx)
library(ggplot2)

```

<!-- rnb-source-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIERFU0NBUkdBIERFTCBBUkNISVZPIERFIElOVEVSTkVUICMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyMjIyNcbmRvd25sb2FkLmZpbGUoXG4gIHVybD1cImh0dHBzOi8vcmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbS9DU1NFR0lTYW5kRGF0YS9DT1ZJRC0xOS9tYXN0ZXIvY3NzZV9jb3ZpZF8xOV9kYXRhL2Nzc2VfY292aWRfMTlfdGltZV9zZXJpZXMvdGltZV9zZXJpZXNfY292aWQxOV9jb25maXJtZWRfZ2xvYmFsLmNzdlwiLGRlc3RmaWxlID1cIkNPVklEMTlfMi5jc3ZcIilcblxuYGBgIn0= -->

```r
#################################### DESCARGA DEL ARCHIVO DE INTERNET ###############################
download.file(
  url="https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv",destfile ="COVID19_2.csv")

```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoicHJvYmFuZG8gbGEgVVJMICdodHRwczovL3Jhdy5naXRodWJ1c2VyY29udGVudC5jb20vQ1NTRUdJU2FuZERhdGEvQ09WSUQtMTkvbWFzdGVyL2Nzc2VfY292aWRfMTlfZGF0YS9jc3NlX2NvdmlkXzE5X3RpbWVfc2VyaWVzL3RpbWVfc2VyaWVzX2NvdmlkMTlfY29uZmlybWVkX2dsb2JhbC5jc3YnXG5Db250ZW50IHR5cGUgJ3RleHQvcGxhaW47IGNoYXJzZXQ9dXRmLTgnIGxlbmd0aCAzMzYzMzggYnl0ZXMgKDMyOCBLQilcbmRvd25sb2FkZWQgMzI4IEtCXG4ifQ== -->

```
probando la URL 'https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_covid19_confirmed_global.csv'
Content type 'text/plain; charset=utf-8' length 336338 bytes (328 KB)
downloaded 328 KB
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->



<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


# Aqui ordenamos los datos por el ultimo mes censado y agregando algunas columnas

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->



<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->


# Observando el puesto por Pais y visualizando algunas metricas

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibnJvdyI6MSwibmNvbCI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVF5MDdETUJEY3BFNVJncWdxOFJzMEVrSGxEQ29jT0JIUmducERKakVRNGRwVjdBRGl4SkV2NGl2Q21iOXBXUWRiQkZ1S1BUdWJmY3hjblMyUGttVUNBQU1nRU1JZ1FnakRXWDZZVFRNQUVtSVVZQ1kyN3l2K3RZK0E0RGZ1SmVJYkp0aGJ3empGWUs5TEFCei80YzhQZkVjR24zdy9IN1J0KytWMWpnUmRNV1c3RWt1Uy9QUmlidkV3dno2Zkx5NXR0THVRbXZMYkdWVlNXV3FVMTNMRnlrcGE5bi8vdUpZdnFadGhsZ3JmOGRyaThSY3BPRlhLazVlVVZOUDB2c1o2akRaZXlZNWM2MG9LTEFxTk41RlhITlFlTVc2RTJhU2NGSStOZUpwa1V6UEJlZ1k5LzRJZUpyOHp3NjN0RlRsYm1IaW9CSFBMYzNySHVETUVKWGVLMDNWZENlMmtJS3RTYmV4elRDRzVZenB4c1BrQkhaMkczaFFDQUFBPSJ9 -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["PAIS"],"name":[1],"type":["chr"],"align":["left"]},{"label":["PUESTO"],"name":[2],"type":["int"],"align":["right"]},{"label":["Total_Casos"],"name":[3],"type":["int"],"align":["right"]},{"label":["Promedio_Casos"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"Venezuela","2":"54","3":"46728","4":"24024.7"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[1]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-frame-begin eyJtZXRhZGF0YSI6eyJjbGFzc2VzIjpbInRibF9kZiIsInRibCIsImRhdGEuZnJhbWUiXSwibnJvdyI6MSwibmNvbCI6NH0sInJkZiI6Ikg0c0lBQUFBQUFBQUJsMVFRVTdETUJEY3BFNVJneWlWZUVjanRSVjNwTUlOcEFoeHlBMjVpU2tXanJmRWlVQ2NlQTJ2Z1MrMXJJTU53WlpzcjhjN3V6dHplMW1zMGlJRmdCRXdpR0dVVUFqamRiNVluaThCV0V5dmlING05bjZsckRNS0dPMlQvZ05BMFo0Tmt0SWJmT1AxUmo1MzRpL3I5SnJ1cVkwdlBvcFBXbDlCNlVUeldoaFhpamx3bW5mQ3RIaGxTdHpLQ2gzS2NpNk5pNC92c09YcWZzME5tbDlTZzdXb0pEcjBmNTlKZ3krWjcyV0hpOS9wT05BS0J5b1ZOeWJVVnZHV1p3OE44ZW0xRHloSHVHc2xhaUxGMXFRa0lFZE5BTXc2YlNlcDV1VmpwNS9tcTRYdDRGeUZnY1BSSUdZL1BlT0RxNVc0V21PaHQxSUxQN3ppRzZHOElTUzVWNXp0R3FsYkw0VlFrN1hXUG8rVXFEelNpNFA5Tnhvemwwc2RBZ0FBIn0= -->

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["PuestoEscogido"],"name":[1],"type":["int"],"align":["right"]},{"label":["Pais"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Total_Casos"],"name":[3],"type":["int"],"align":["right"]},{"label":["Promedio_Casos"],"name":[4],"type":["dbl"],"align":["right"]}],"data":[{"1":"108","2":"Mozambique","3":"3916","4":"2860.4"}],"options":{"columns":{"min":{},"max":[10],"total":[4]},"rows":{"min":[10],"max":[10],"total":[1]},"pages":{}}}
  </script>
</div>

<!-- rnb-frame-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->



<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-plot-begin eyJoZWlnaHQiOjQzMi42MzI5LCJ3aWR0aCI6NzAwLCJzaXplX2JlaGF2aW9yIjowLCJjb25kaXRpb25zIjpbXX0= -->

<img src="data:image/png;base64,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" />

<!-- rnb-plot-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->




# Prediccion con Learner

<!-- rnb-text-end -->


<!-- rnb-chunk-begin -->


<!-- rnb-source-begin eyJkYXRhIjoiYGBgclxuICBwcmVkaWNjaW9uZXM9U3VwZXJMZWFybmVyKHksWCxmYW1pbHkgPSBnYXVzc2lhbigpLFxuICAgICAgICAgICAgICAgICAgICAgICAgICAgIFNMLmxpYnJhcnk9YyhcIlNMLnJhbmRvbUZvcmVzdFwiLFwiU0wuY2FyZXRcIikpIFxuXG5gYGAifQ== -->

```r
  predicciones=SuperLearner(y,X,family = gaussian(),
                            SL.library=c("SL.randomForest","SL.caret")) 

```

<!-- rnb-source-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDEwIG9uIGZ1bGwgdHJhaW5pbmcgc2V0XG4ifQ== -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 10 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDEwIG9uIGZ1bGwgdHJhaW5pbmcgc2V0XG4ifQ== -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 10 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDEwIG9uIGZ1bGwgdHJhaW5pbmcgc2V0XG4ifQ== -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 10 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDYgb24gZnVsbCB0cmFpbmluZyBzZXRcbiJ9 -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 6 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDYgb24gZnVsbCB0cmFpbmluZyBzZXRcbiJ9 -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 6 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDEwIG9uIGZ1bGwgdHJhaW5pbmcgc2V0XG4ifQ== -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 10 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDEwIG9uIGZ1bGwgdHJhaW5pbmcgc2V0XG4ifQ== -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 10 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDYgb24gZnVsbCB0cmFpbmluZyBzZXRcbiJ9 -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 6 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDEwIG9uIGZ1bGwgdHJhaW5pbmcgc2V0XG4ifQ== -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 10 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDIgb24gZnVsbCB0cmFpbmluZyBzZXRcbiJ9 -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 2 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiKyBGb2xkMDE6IG10cnk9IDIgXG4ifQ== -->

```
+ Fold01: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDIgXG4rIEZvbGQwMTogbXRyeT0gNiBcbiJ9 -->

```
- Fold01: mtry= 2 
+ Fold01: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9IDYgXG4rIEZvbGQwMTogbXRyeT0xMCBcbiJ9 -->

```
- Fold01: mtry= 6 
+ Fold01: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDE6IG10cnk9MTAgXG4rIEZvbGQwMjogbXRyeT0gMiBcbiJ9 -->

```
- Fold01: mtry=10 
+ Fold02: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDIgXG4rIEZvbGQwMjogbXRyeT0gNiBcbiJ9 -->

```
- Fold02: mtry= 2 
+ Fold02: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9IDYgXG4rIEZvbGQwMjogbXRyeT0xMCBcbiJ9 -->

```
- Fold02: mtry= 6 
+ Fold02: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDI6IG10cnk9MTAgXG4rIEZvbGQwMzogbXRyeT0gMiBcbiJ9 -->

```
- Fold02: mtry=10 
+ Fold03: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDIgXG4rIEZvbGQwMzogbXRyeT0gNiBcbiJ9 -->

```
- Fold03: mtry= 2 
+ Fold03: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9IDYgXG4rIEZvbGQwMzogbXRyeT0xMCBcbiJ9 -->

```
- Fold03: mtry= 6 
+ Fold03: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDM6IG10cnk9MTAgXG4rIEZvbGQwNDogbXRyeT0gMiBcbiJ9 -->

```
- Fold03: mtry=10 
+ Fold04: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDIgXG4rIEZvbGQwNDogbXRyeT0gNiBcbiJ9 -->

```
- Fold04: mtry= 2 
+ Fold04: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9IDYgXG4rIEZvbGQwNDogbXRyeT0xMCBcbiJ9 -->

```
- Fold04: mtry= 6 
+ Fold04: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDQ6IG10cnk9MTAgXG4rIEZvbGQwNTogbXRyeT0gMiBcbiJ9 -->

```
- Fold04: mtry=10 
+ Fold05: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDIgXG4rIEZvbGQwNTogbXRyeT0gNiBcbiJ9 -->

```
- Fold05: mtry= 2 
+ Fold05: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9IDYgXG4rIEZvbGQwNTogbXRyeT0xMCBcbiJ9 -->

```
- Fold05: mtry= 6 
+ Fold05: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDU6IG10cnk9MTAgXG4rIEZvbGQwNjogbXRyeT0gMiBcbiJ9 -->

```
- Fold05: mtry=10 
+ Fold06: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDIgXG4rIEZvbGQwNjogbXRyeT0gNiBcbiJ9 -->

```
- Fold06: mtry= 2 
+ Fold06: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9IDYgXG4rIEZvbGQwNjogbXRyeT0xMCBcbiJ9 -->

```
- Fold06: mtry= 6 
+ Fold06: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDY6IG10cnk9MTAgXG4rIEZvbGQwNzogbXRyeT0gMiBcbiJ9 -->

```
- Fold06: mtry=10 
+ Fold07: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDIgXG4rIEZvbGQwNzogbXRyeT0gNiBcbiJ9 -->

```
- Fold07: mtry= 2 
+ Fold07: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9IDYgXG4rIEZvbGQwNzogbXRyeT0xMCBcbiJ9 -->

```
- Fold07: mtry= 6 
+ Fold07: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDc6IG10cnk9MTAgXG4rIEZvbGQwODogbXRyeT0gMiBcbiJ9 -->

```
- Fold07: mtry=10 
+ Fold08: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDIgXG4rIEZvbGQwODogbXRyeT0gNiBcbiJ9 -->

```
- Fold08: mtry= 2 
+ Fold08: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9IDYgXG4rIEZvbGQwODogbXRyeT0xMCBcbiJ9 -->

```
- Fold08: mtry= 6 
+ Fold08: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDg6IG10cnk9MTAgXG4rIEZvbGQwOTogbXRyeT0gMiBcbiJ9 -->

```
- Fold08: mtry=10 
+ Fold09: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDIgXG4rIEZvbGQwOTogbXRyeT0gNiBcbiJ9 -->

```
- Fold09: mtry= 2 
+ Fold09: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9IDYgXG4rIEZvbGQwOTogbXRyeT0xMCBcbiJ9 -->

```
- Fold09: mtry= 6 
+ Fold09: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMDk6IG10cnk9MTAgXG4rIEZvbGQxMDogbXRyeT0gMiBcbiJ9 -->

```
- Fold09: mtry=10 
+ Fold10: mtry= 2 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDIgXG4rIEZvbGQxMDogbXRyeT0gNiBcbiJ9 -->

```
- Fold10: mtry= 2 
+ Fold10: mtry= 6 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9IDYgXG4rIEZvbGQxMDogbXRyeT0xMCBcbiJ9 -->

```
- Fold10: mtry= 6 
+ Fold10: mtry=10 
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiLSBGb2xkMTA6IG10cnk9MTAgXG5BZ2dyZWdhdGluZyByZXN1bHRzXG5TZWxlY3RpbmcgdHVuaW5nIHBhcmFtZXRlcnNcbkZpdHRpbmcgbXRyeSA9IDIgb24gZnVsbCB0cmFpbmluZyBzZXRcbiJ9 -->

```
- Fold10: mtry=10 
Aggregating results
Selecting tuning parameters
Fitting mtry = 2 on full training set
```



<!-- rnb-output-end -->

<!-- rnb-output-begin eyJkYXRhIjoiU2V0dGluZyByb3cgbmFtZXMgb24gYSB0aWJibGUgaXMgZGVwcmVjYXRlZC5cbiJ9 -->

```
Setting row names on a tibble is deprecated.
```



<!-- rnb-output-end -->

<!-- rnb-chunk-end -->


<!-- rnb-text-begin -->





<!-- rnb-text-end -->

