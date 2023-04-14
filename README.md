# parcial_bioinformatica
## Parcial Bionformatica Valentina Aguilar 

## Punto 1
- Descarga del query = wget https://raw.githubusercontent.com/paula-torres/bioinformatica_ur/main/files/query_parcial.fasta
- El popset lo descargue de forma manual desde el NCBI, buscando por el numero 1776322181. 
- Modifique la información de los encabezados en Atom: Buscando : (>\w*\.\d)\s(\w*)\s(\w*)\s(\w*)\s(\w*\-\d)\s\w.* reemplazando por $1_COI_$2_$3_$4_$5
- Subi el archivo al cluster: scp -r -i bio.pt.pem -P 37022 /mnt/c/Users/valea/OneDrive/Documents/Bioinformatica/Parcial bio.pt@172.25.255.10:/home/bio.pt/data/Parcial1/parcial1_ValentinaAguilar

Ya en el cluster

- Genere la base de datos de blast = makeblastdb -in sequence.fasta -dbtype nucl -parse_seqids -out trans_sequence -title "secuence_parcial"
- Genere el blastn con el query = = blastn -query query_parcial.fasta -task megablast -db trans_sequence -outfmt 7 -word_size 7 -out blastn -num_threads 1

![image](https://user-images.githubusercontent.com/127573975/232137662-301ecc23-8cb7-4f3e-9acb-91bcd5693c6a.png)

- Interpretación: Llevando a cabo el blast con el query, se encontraron 67 concurrencias, entre ellos el encuentro mas alto se da con _MK860946.1_COI_Spodoptera_cilium_isolate_MA-6_, la cual cuenta con un porcentaje de identidad cercano al 96%. Al mismo tiempo se ve que consta de 21 desajustes. La cual la posiciona en el segundo con mayor cantidad. Por otro lado, no tiene ningún gap abierto, es decir que la secuencia es continua. De la misma forma, indica que la probabilidad de que este alineamiento se de por azar es cercano al 0.

## Punto 2 
En la terminal 
- Concatene las secuencias con = cat query_parcial.fasta sequence.fasta > concatenado.fasta
- Alineamiento con Clustal, usando el concatenado como inicial orden de opciones (1,2,9,F,1) 
- Genere una subcarpeta con el fasconcat y el alineamiento. Corri el fasconcat con  ./FASconCAT-G_v1.05.1.pl. cambiando los parametros (N y P ). Despues corri el iqtree con: iqtree -s FcC_supermatrix.phy -m GTR+I+G -bb 1000 -pre arbol

![image](https://user-images.githubusercontent.com/127573975/232140119-0cddd088-2e47-433e-8962-7a6b01986d63.png)

•	La secuencia de query se agrupa junto a spodoptera en un clado sepadado, con un soporte del 56%, por otro lado, la longitud de la rama de query es un poco mas amplia que la de spodoptera, lo que puede indicar un mayor tiempo de divergencia o una mayor diferencia en la historia evolutiva. 
•	Spodoptera se podría considerar como un grupo monofilético, si tenemos en cuenta que en el punto anterior al hacer el bast esta tenia una mayor probabilidad de corresponder a otra spodoptera. En el grupo inferior de este genero, las ramas son mas pequeñas, por lo que se podría decir que tienen un tiempo de divergencia mas corto, junto con una historia evolutiva similar. Por otro lado al comparar la rama superior con la inferior el tiempo se divergencia es almplio 
•	La siguiente es de Peridroma, que se puede considerar tambien como un clado monofilético con un soporte de 100%, son solo dos especies hermanas, con un tiempo de divergencia mas alto en relación con la rama de abajo. Tambien se puede decir que por la longitud de las ramas entre las especies hermanas hay una historia evolutiva similar 
•	Por ultimo la rama inferior tambien se puede considerar como monofilética, con un soporte entre 100 y 51 %, de la misma forma la longitud de las ramas indica que tienen una historia evolutiva similar, y que este grupo es mas cercano a Peridroma que a Spodoptera. 

## Punto 3 

- descargue el archivo en mi computador con wget https://raw.githubusercontent.com/paula-torres/bioinformatica_ur/main/files/archivo1.csv
- wc -L archivo1.csv = el archivo tiene 20 lineas 
- awk -F"\," '{print NF; exit}' archivo1.csv = tiene 4 columnas 
- wc -m archivo1.csv = tiene 908 caracteres 
- cambio de Chr por cromosoma = sed -i 's/chr/cromosoma/' archivo1.csv
- cambio de comas por tabulaciones = lo hice en atom = (found:  ,) (replace: t)
- Guardar solo aquellos que contengan coding= lo hice en el archivo delimitado por comas = grep -e ",coding" archivo1.csv.1  > result_file_coding.bed, y en el archivo separado por tabulación =  grep -e "\scoding" archivo1.csv > resultresult_file_coding2.bed

## Punto 4 
- Organice los archivos en carpetas por puntos, despues comprimi toda la carpeta con zip -r desde la terminal 
- Descargue la carpeta al computador con = scp -r -i bio.pt.pem -P 37022 bio.pt@172.25.255.10://home/bio.pt/data/Parcial1/parcial1_ValentinaAguilar/parcial_ValentinaAguilar.zip /mnt/c/Users/valea/OneDrive/Documents/Bioinformatica 

- Y la subi al Git Hub de forma manual. 


