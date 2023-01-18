# HW1 (Aksenov Yaroslav)

1. Создаю ссылки на файлы:<br>
  ```bash
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq
    ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
  ```
2. С моим seed'ом 1217 и случайно беру 5 миллионов paired-end чтений и 1.5 миллиона mate-pairs чтений
  ```bash
    seqtk sample -s1217 oil_R1.fastq 5000000 > sub1.fastq
    seqtk sample -s1217 oil_R2.fastq 5000000 > sub2.fastq
    seqtk sample -s1217 oilMP_S4_L001_R1_001.fastq 1500000 > matepairs.fastq
    seqtk sample -s1217 oilMP_S4_L001_R2_001.fastq 1500000 > matepairs2.fastq
  ```
3. Оцениваю качество данных и получаю статистику с помощью fastQC и multiQC:
  ```bash
    mkdir fastqc
    ls sub* matepairs* | xargs -tI{} fastqc -o fastqc {}
    mkdir multiqc
    multiqc -o multiqc fastqc
  ```
5. Подрезаю чтения по качеству и удаляю адаптеры:<br>
  ```bash
    platanus_trim sub*
    platanus_internal_trim matepair*
  ```
6. Удаляю .fastq файлы
  ```bash
    rm sub1.fastq
    rm sub2.fastq
    rm matepairs.fastq 
    rm matepairs2.fastq
  ```
7. Оцениваю качество подрезанных данных и считаю статистику:<br>
  ```bash
    mkdir fastqc_trim
    ls sub* matepairs*| xargs -tI{} fastqc -o fastqc_trim {}
    mkdir multqctrim
    multiqc -o multqctrim fastqc_trim
  ```
9. Используя platanus assemble собираю контиги:<br>
  ```bash
  time platanus assemble -o Poil -f sub1.fastq.trimmed sub2.fastq.trimmed 2> assemble.log
  ```
10. Используя platanus scaffold собираю скаффолды:<br>
  ```bash
  time platanus scaffold -o Poil -c Poil_contig.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matepairs.fastq.int_trimmed matepairs2.fastq.int_trimmed 2> scaffold.log
  ```
11. Используя platanus gap_close уменьшаю гэпы:
  ```bash
  time platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub1.fastq.trimmed sub2.fastq.trimmed -OP2 matepairs.fastq.int_trimmed  matepairs2.fastq.int_trimmed 2> gapclose.log
  ```

### <p align=center> Оцениваем качество </p>
#### <p align=center> Исходные чтения </p>
<img src="https://github.com/yaraksen/hse22_hw1/blob/master/images/general_stats.png"/>
<img src="https://github.com/yaraksen/hse22_hw1/blob/master/images/per_seq_stats.png"/>

#### <p align=center> Подрезанные чтения </p>
<img src="https://github.com/yaraksen/hse22_hw1/blob/master/images/trim_general_stats.png"/>
<img src="https://github.com/yaraksen/hse22_hw1/blob/master/images/trim_per_seq_stats.png"/>