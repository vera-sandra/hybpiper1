#Hybpiper# 

##Preprocesamiento de muestras##

El presente tutorial corresponde al manejo de muestras obtenidas de la técnica de partición de genomas Enriquecimiento Híbrido Anclado  [(AHE)](https://academic.oup.com/sysbio/article/61/5/727/1737120) procesadas en la plataforma de secuenciación de nueva generación  [Illumina HiSeq2500](https://www.illumina.com/systems/sequencing-platforms/hiseq-2500.html).

###Programas requeridos
Antes de comenzar es necesario corroborar que los siguientes programas  se encuentren instalados en  la PC a utilizar  o corroborar que sean soportados para su posterior instalación:

-**[Phython](https://www.python.org/)**

-**[Putty](https://www.ssh.com/ssh/putty/)**

-**[FileZilla](https://filezilla-project.org/)**

-**[Trimomatic](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf)** 

___

#####*Descarga de secuencias*
En general una vez que tus muestras se han secuenciado la empresa envía a tu correo las instrucciones para descargar las secuencias, una por una  o de manera simultánea.

- Ingresa a **putty** y crea un nuevo directorio  (nueva carpeta), puede ser el nombre de tu grupo de trabajo.

-El siguiente es un ejemplo `mkdir Bromeliaceae`.

-Ve a tu nuevo directorio de trabajo  `cd Bromeliaceae`  y crea una nueva carpeta  p.e `mkdir secuenciasOriginales`.


- Utiliza **FileZilla** para arrastrar las secuencias descargadas desde su ubicación al directorio de trabajo ` secuenciasOriginales` en la terminal.

-En la consola puedes utilizar el comando `ls -l` para visualizar en forma de lista las secuencias que ahora contiene tu carpeta `secuenciasOriginales`.

#####*Renombra*

En este ejemplo la secuenciación fue bidireccional por lo cual se tendrán dos secuencias para el mismo individuo, una en cada dirección.

- Utiliza el comando `mv` para cambiar el nombre de las secuencias **utiliza mínimo 8 caracteres** para facilitar tus análisis posteriores.

-Recuerda que el *forward* (R1) y *reverse* (R2) deben tener el mismo nombre ya que son secuencias complementarias de un mismo individuo. Coloca el nombre de tu archivo tal cual aparece en tu directorio, deja un espacio, y coloca el nuevo nombre de tu secuencia siempre al inicio. 

```
mv JDUAAKD_S4_1_MYEYSB_CGM1086.fastq.gz violaceae_JDUAAKD_S4_1_MYEYSB_CGM1086.fastq.gz
``` *forward*

```
mv JDUAAKD_S4_2_MYEYSB_CGM1086.fastq.gz violaceae_JDUAAKD_S4_2_MYEYSB_CGM1086.fastq.gz
``` *reverse*

-Repite para todas tus muestras.

```
mv HGTAAKD_S4_1_MYEYSB_CGM865.fastq.gz utricula_HGTAAKD_S4_1_MYEYSB_CGM1086.fastq.gz
``` 

```
mv HGTAAKD_S4_2_MYEYSB_CGM865.fastq.gz utricula_HGTAAKD_S4_2_MYEYSB_CGM1086.fastq.gz
``` 

```
mv FGBAAKD_S4_1_MYEYSB_CGM865.fastq.gz ionantha_FGBAAKD_S4_1_MYEYSB_GAS670.fastq.gz
```

```
mv FGBAAKD_S4_2_MYEYSB_GAS670.fastq.gz ionantha_FGBAAKD_S4_2_MYEYSB_GAS670.fastq.gz
```


```
mv KAHAAKD_S4_1_MYEYSB_CGM716.fastq.gz makoyana_KAHAAKD_S4_1_MYEYSB_CGM716.fastq.gz
```

```
mv KAHAAKD_S4_2_MYEYSB_CGM716.fastq.gz makoyana_KAHAAKD_S4_2_MYEYSB_CGM716.fastq.gz
```


```
mv YJUAAKD_S4_1_MYEYSB_CGM865.fastq.gz recurvat_YJUAAKD_S4_1_MYEYSB_CGM865.fastq.gz
```

```
mv YJUAAKD_S4_2_MYEYSB_CGM865.fastq.gz recurvat_YJUAAKD_S4_2_MYEYSB_CGM865.fastq.gz
```

___


#####*Filtra*

- Utiliza los comandos de **[Trimomatic](http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/TrimmomaticManual_V0.32.pdf)** para:

-`LEADING` remover las bases de baja calidad al inicio de la secuencia.

-`TRAILING` remover las bases de baja calidad al final de la secuencia.

-`SLIDINGWINDOW` remover bases de baja calidad al interior de la secuencia.

-`MINLEN` remover las lecturas por debajo de una longitud mínima requerida.

El siguiente comando contiene los parámetro básicos. Observa que utiliza las lecturas con ambos sentidos como archivos de entrada y la instrucción *paired* y *unpaired* para los archivos de salida. 

```
java -jar [path to trimmomatic jar] PE [input 1] [input 2] [paired output1] [unpaired output1] [paired output2] [unpaired output2] LEADING:3 TRAILING:3 SLIDINGWINDOW:4:20 MINLEN:30
```

Ejemplo para el primer individuo

```
java -jar [path to trimmomatic jar] PE [violaceae_JDUAAKD_S4_1_MYEYSB_CGM1086.fastq.gz] [violaceae_JDUAAKD_S4_2_MYEYSB_CGM1086.fastq.gz] [paired violaceae_JDUAAKD_S4_1_MYEYSB_CGM1086.fastq.gz] [unpaired violaceae_JDUAAKD_S4_1_MYEYSB_CGM1086.fastq.gz] [paired violaceae_JDUAAKD_S4_2_MYEYSB_CGM1086.fastq.gz] [unpaired violaceae_JDUAAKD_S4_2_MYEYSB_CGM1086.fastq.gz] LEADING:3 TRAILING:3 SLIDINGWINDOW:4:20 MINLEN:30
```

#####*Descomprime*

- Descomprime todas las secuencias en formato gzip. Puedes utilizar el siguiente comando para descomprimir al mismo tiempo todas las secuencias. 

`gzip -d *.fastq.gz`



___
¡A partir de aquí ya puedes empezar tu procesamiento!