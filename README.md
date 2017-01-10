# Estaciones-IDEAM


# Es importante que se cargue el tr5 porque es el que tiene los valores de los dias sin encabezado para el caso de R

Archivo_crudo = tr5

tablaIDEAM = data.frame(id = substr(Archivo_crudo$V1, 0, 1), cod = substr(Archivo_crudo$V1, 2, 9), 
                        tipo = substr(Archivo_crudo$V1, 10, 11), ano = c(substr(Archivo_crudo$V1, 12, 15)), 
                        d_info = substr(Archivo_crudo$V1, 16, 17), 
                        ene = substr(Archivo_crudo$V1, 18, 22), ene_or = substr(Archivo_crudo$V1, 23, 23), 
                        feb = substr(Archivo_crudo$V1, 24, 28), feb_or = substr(Archivo_crudo$V1, 29, 29), 
                        mar = substr(Archivo_crudo$V1, 30, 34), mar_or = substr(Archivo_crudo$V1, 35, 35), 
                        abr = substr(Archivo_crudo$V1, 36, 40), abr_or = substr(Archivo_crudo$V1, 41, 41), 
                        may = substr(Archivo_crudo$V1, 42, 46), may_or = substr(Archivo_crudo$V1, 47, 47), 
                        jun = substr(Archivo_crudo$V1, 48, 52), jun_or = substr(Archivo_crudo$V1, 53, 53), 
                        jul = substr(Archivo_crudo$V1, 54, 58), jul_or = substr(Archivo_crudo$V1, 59, 59), 
                        ago = substr(Archivo_crudo$V1, 60, 64), ago_or = substr(Archivo_crudo$V1, 65, 65), 
                        spt = substr(Archivo_crudo$V1, 66, 70), spt_or = substr(Archivo_crudo$V1, 71, 71), 
                        oct = substr(Archivo_crudo$V1, 72, 76), oct_or = substr(Archivo_crudo$V1, 77, 77), 
                        nov = substr(Archivo_crudo$V1, 78, 82), nov_or = substr(Archivo_crudo$V1, 83, 83), 
                        dic = substr(Archivo_crudo$V1, 84, 88), dic_or = substr(Archivo_crudo$V1, 89, 89), 
                        
                        esp_b = substr(Archivo_crudo$V1, 90, 99), 
                        t_dat = substr(Archivo_crudo$V1, 100, 22)
)

tablaIDEAM[tablaIDEAM == 99999] = NA

View(tablaIDEAM)

IDEAM_Cundinamarca2 = tablaIDEAM

str(IDEAM_Cundinamarca2)

for(i in 4:31){
    IDEAM_Cundinamarca2[,i] = as.numeric(as.character(IDEAM_Cundinamarca2[,i]))
}


str(IDEAM_Cundinamarca2)

#lista_nombres = function(data1){ as.data.frame(names(data1))}
#lista_nombres(IDEAM_Cundinamarca2)

cat_IDEAM <- read.delim("~/Descargas/CATALOGO_ESTACIONES_IDEAM__V8_SEPT_01_2016 (1).csv")

union_1 = merge(x = IDEAM_Cundinamarca2, y = cat_IDEAM, by = "cod", all.x = T)
View(union_1)

union_1$LATITUD = as.numeric(as.character(union_1$LATITUD))
union_1$LONGITUD = as.numeric(as.character(union_1$LONGITUD))


union_2 = union_1[which(!is.na(union_1$LATITUD)),]
View(union_2)
