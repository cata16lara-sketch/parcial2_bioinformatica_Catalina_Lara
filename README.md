# parcial2_bioinformatica_Catalina_Lara
Parcial 2
# PRIMER PUNTO (1)
Para evaluar la calidad de las lecturas crudas obtenidas, se utilizó el software FastQC. 
El comando utilizado es:
# fastqc *.fastq.gz
Por cada archivo FASTQ se generaron los siguientes reportes:
# SRR8528336_1_fastqc.html
# SRR8528336_1_fastqc.zip
# SRR8528336_2_fastqc.html
# SRR8528336_2_fastqc.zip
Se descargaron los archivos .html
file://wsl$/Ubuntu/root/SRR8528336_1_fastqc.html
file://wsl$/Ubuntu/root/SRR8528336_2_fastqc.html
Para evaluar la calidad de las lecturas se utilizó el software FastQC.
A partir de este análisis se observó que los archivos SRR8528336_1.fastq.gz y SRR8528336_2.fastq.gz contienen cada uno 500,000 secuencias, 
sin lecturas marcadas como de baja calidad, con una longitud uniforme de 101 pb y un contenido GC de 43%, lo cual se encuentra dentro de lo esperado y no sugiere problemas de contaminación. 
En cuanto a la calidad por base, la mayoría de las posiciones presentan valores de Phred mayores a 30,
lo que indica que las lecturas son confiables.
También se observa que la calidad se mantiene bastante estable a lo largo de la secuencia.
# PRIMER PUNTO (2)
Se Utilizo SPAdes para realizar el ensamblaje de novo utilizando los reads, en un sbatch con este código:
#!/bin/sh
#SBATCH -p normal #Particion (cola)
#SBATCH -N 1 # Numero de nodos
#SBATCH -n 8 # Numero de nucleos
#SBATCH -t 1-20:00 # limite de tiempo (D-HH:MM)
#SBATCH -o salida.out # Salida STDOUT
#SBATCH -e error.err # Salida STDERR
#SBATCH --mail-user=laurac.lara@urosario.edu.co #Direccion e-mail a donde notificar el estado del trabajo
#SBATCH --mail-type=ALL #Especifica que eventos notificar al correo (ALL, BEGIN, END, REQUEUE, FAIL)

module load spades
spades.by -1 SRR8528336_1.fastq.gz -2 SRR8528336_2.fastq.gz -o ensamblaje_spades

