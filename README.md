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
luego de esperar a que corriera obtuvimos los scaffolds
# PRIMER PUNTO (3)
Una vez finalizado el ensamblaje de novo, se calcularon las estadísticas del ensamblaje utilizando el software QUAST, a partir del archivo de scaffolds generado por SPAdes.
El comando utilizado fue:
# /datacnmat01/ciencias/appsbio/conda/pkgs/quast-5.2.0-py39pl5321h4e691d4_3/opt/quast-5.2.0/quast.py scaffolds.fasta -o quast_results
Resultados 
<img width="239" height="313" alt="image" src="https://github.com/user-attachments/assets/f2cc7ef3-3e33-4025-b2f3-d77cebb9fd1e" />
A partir de los resultados obtenidos, el ensamblaje presenta un tamaño total de 2,109,361 pb. El valor de N50 (1,329 pb) indica que la mitad del ensamblaje está contenida en scaffolds de al menos esa longitud, lo cual sugiere que los fragmentos obtenidos no son muy largos. Por otro lado, el valor de L50 (454) indica que se requieren 454 scaffolds para cubrir el 50% del genoma ensamblado, lo que refleja un alto nivel de fragmentación.En general, esto sugiere que el ensamblaje tiene una contigüidad baja.



