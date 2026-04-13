# HW1 -- Summary (*Bacillus subtilis* 168)

**Student:** `ro-sveta`
**Run dir:** `stud05/day8/blastim/outputs/run_latest/`
**Assigned genes file:** `genes_ro-sveta.txt` (12 генов)

> **Правило:** На каждый ген 4 строки: Prokka → DIAMOND → Pfam → вывод.
>
> **Минимум:** По 1 гену в каждом из 6 блоков (всего 6 генов). Можете добавить больше.

---

## 1) Репликация / ремонт ДНК

### Gene: `OHEIKNII_00140`
- **Prokka product:** Elongation factor Tu
- **DIAMOND:** pident=30.6%, evalue=1.09e-25, coverage=87.4%, hit: Sulfate adenylyltransferase subunit 1
- **Pfam:** Elongation factor Tu GTP binding domain (PF00009.34, 2.6e-69)
- **Вывод:** Аннотация ориентировочная, так как pident около 30%, покрытие высокое, что говорит о совпадении с доменом, а не всей белковой последовательностью

---

## 2) Транскрипция / трансляция (housekeeping)

### Gene: `OHEIKNII_02062` (опционально)
- **Prokka product:** Transcriptional regulatory protein DesR
- **DIAMOND:** pident=26.4%, evalue=2.27e-18, coverage=101%, hit: Virulence factors putative positive transcription regulator
- **Pfam:** Response regulator receiver domain (PF00072.31, 1.4e-26), Bacterial regulatory proteins, luxR family (PF00196.26, 1.9e-21)
- **Вывод:** Аннотация не поддерживается из-за низкой идентичности, несмотря на высокое покрытие и низкое значение e-value

---

## 3) Метаболизм (путь: ____________________)

### Gene: `OHEIKNII_02470`
- **Prokka product:** Thiol-disulfide oxidoreductase ResA
- **DIAMOND:** 	pident=26.5%, evalue=2.55e-10, coverage=27.4%, hit: Putative peroxiredoxin MT2597 OS=Mycobacterium tuberculosis
- **Pfam:** AhpC/TSA family (PF00578.28, e=3.4e-37), Thioredoxin (PF00085.27, e=1.2e-10)
- **Вывод:** аннотация не поддерживается из-за низкого покрытия и идентичности, несмотря на низкое значение e-value

### Gene: `OHEIKNII_02921` (опционально — удалите если используете 1 ген на блок)
- **Prokka product:** Cysteine desulfurase IscS
- **DIAMOND:** pident=27.5%, evalue=1.31e-37, coverage=104.5%, hit: Probable cysteine desulfurase OS=Halobacterium salinarum
- **Pfam:** Aminotransferase class-V (PF00266.26, 2.1e-87), Aminotransferase class I and II (PF00155.28, 6.6e-07)
- **Вывод:** Аннотация не поддерживается из-за низкой идентичности, несмотря на высокое покрытие и низкое значение e-value

---

## 4) Транспорт / мембраны

### Gene: `OHEIKNII_00820` (опционально)
- **Prokka product:** putative ABC transporter ATP-binding protein YbiT
- **DIAMOND:** pident=35.9%, evalue=2.86e-90, coverage=99%, hit: ABC transporter F family member 2
- **Pfam:** ABC transporter (PF00005.34, 2.8e-55)
- **Вывод:** аннотация, скорее, поддерживается высокими значением покрытия, низким значением e-value и значением идентичности выше 30%

### Gene: `OHEIKNII_04165`
- **Prokka product:** 	putative amino-acid permease protein YxeN
- **DIAMOND:** pident=30.6%, evalue=4.59e-31, coverage=96.4%, hit: Arginine transport system permease protein
- **Pfam:** Binding-protein-dependent transport system inner membrane component (PF00528, e=1.3e-29)
- **Вывод:** pident=30% identity - это граница «сумеречной зоны», так как покрытие высокое, можно предположить, что совпал только домен, а не весь белок

### Gene: `OHEIKNII_03556`
- **Prokka product:** Cadmium, zinc and cobalt-transporting ATPase
- **DIAMOND:** pident=99.9%, evalue=0, coverage=100%, hit: Cadmium, zinc and cobalt-transporting ATPase
- **Pfam:** P-type ATPase actuator domain (PF00122.26, 2.1e-28), Heavy-metal-associated domain (PF00403.33, 1.5e-11)
- **Вывод:** точная аннотация поддерживается полностью данными.

---

## 5) Регуляция

### Gene: `OHEIKNII_03688`
- **Prokka product:** Thioredoxin reductase
- **DIAMOND:** pident=33.4%, evalue=6.06e-54, coverage=98.4%, hit: Alkyl hydroperoxide reductase subunit F
- **Pfam:** Pyridine nucleotide-disulphide oxidoreductase (PF00070.34, 2.1e-22)
- **Вывод:** аннотация скорре поддерживается (высокие значения покрытия, низкие значения e-value и значение идентичности выше 30%)

### Gene: `OHEIKNII_01967` (опционально)
- **Prokka product:** Plipastatin synthase subunit B
- **DIAMOND:** pident=40.9%, evalue=0, coverage=100%, hit: Bacitracin synthase 3 OS=Bacillus licheniformis
- **Pfam:** AMP-binding enzyme (PF00501.35, 2.3e-184)
- **Вывод:** аннотация поддерживается данными

---

## 6) Стресс-ответ / споры (если нашли)

### Gene: `OHEIKNII_01397`
- **Prokka product:** putative glycosyltransferase
- **DIAMOND:** pident=38.7%, evalue=6.04e-70, coverage=96%, hit: Putative glycosyltransferase CsbB
- **Pfam:** Glycosyl transferase family 2 (PF00535.33, 5.6e-41)
- **Вывод:** аннотация полностью поддерживается

### Gene: `OHEIKNII_01281` (опционально)
- **Prokka product:** putative N-acetyltransferase YjcF
- **DIAMOND:** pident=47.4%, evalue=8.12e-31, coverage=96.4% hit: Putative acetyltransferase BSU40680
- **Pfam:** Acetyltransferase (GNAT) family (PF00583.32, 4.8e-16)
- **Вывод:** аннотация полностью поддерживается

### Gene: `OHEIKNII_02807` (опционально)
- **Prokka product:** hypothetical protein
- **DIAMOND:** pident=18.9%, evalue=3.65e-06, coverage=52.8%, hit: Sensor histidine kinase CusS
- **Pfam:** His Kinase A (phospho-acceptor) domain (PF00512.32, 9.7e-11)
- **Вывод:** аннотация не поддерживается (низкие значения pident и coverage)

---

## Общий вывод (3-5 предложений)

- Что у штамма "явно хорошо видно" по аннотации:
- Где больше неопределённости и почему:
- Какие 1-2 шага добавили бы уверенности (что бы вы сделали дальше):
У штамма хорошо прослеживаются гены, связанные с транспортом, метаболизмом тяжелых металлов и стресс-ответами, что свидетельствует о его устойчивости к неблагоприятным факторам и высокой адаптивности. В то же время, существует значительная неопределенность в функции некоторых генов, связанных с регуляцией и репликацией, из-за низкой идентичности и покрытия в аннотациях. Чтобы повысить уверенность, стоит провести дополнительную проверку этих участков.