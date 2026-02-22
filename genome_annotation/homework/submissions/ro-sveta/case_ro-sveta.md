# HW1 -- Case investigation (one gene)

**Student:** `ro-sveta`
**Run dir:** `stud05/day8/blastim/outputs/run_latest/`

> **Справочник:** См. `docs/glossary.md` для терминов (паралогия, CDS, оперон, синтения, KO/COG).
> **Полное задание:** См. `docs/homework_01.md` для контекста (это Part 2 из HW1).

---

## Что такое case investigation?

Это глубокий разбор **одного** гена из вашего assigned списка, у которого аннотация Prokka вызывает сомнения. Вы собираете все доказательства (DIAMOND + Pfam) и предлагаете более честную аннотацию.

**Цель:** Научиться критически оценивать автоматические аннотации и использовать "лесенку доказательств" для обоснованного вывода.

---

## 0) Gene ID

- **Gene/Protein ID:** OHEIKNII_02807

---

## 1) Текущая аннотация Prokka

- **Prokka product** (как записано в GFF/TSV): hypothetical protein
- **Длина белка** (aa), если известна: 432 aa

---

## 2) DIAMOND evidence

Вставьте **одну строку** из `blastp_results.tsv` (лучший hit):

```
OHEIKNII_02807	sp|Q8XBY4|CUSS_ECO57	18.9ם	228	177	2	155	382	195	414	3.65e-06	50.4	sp|Q8XBY4|CUSS_ECO57 Sensor histidine kinase CusS OS=Escherichia coli O157:H7 OX=83334 GN=cusS PE=3 SV=1
```

- **pident:** 18.9%
- **evalue:** 3.65e-06
- **length (alignment) / qlen (query length):** 228 / 432 (coverage = 52.8%)
- **stitle (best hit):** Sensor histidine kinase CusS [Escherichia coli]

**Интерпретация (1-2 предложения):**
В данном случае выявлен низкий pident (гораздо ниже 60%), что указывает на неродственный белок

**Критерии оценки:**
- pident **≥80%** + evalue **<1e-10** + coverage **≥70%** → сильное доказательство
- pident **60-80%** или coverage **<70%** → умеренное (возможно паралог или только домен)
- pident **<60%** → слабое (скорее всего неродственный белок)

---

## 3) Pfam/HMMER evidence

Домены из `hmmscan_domtblout.txt`:

- **Domain 1:** His Kinase A (phospho-acceptor) domain (PF00512.32, 9.7e-11)
- **Domain 2:** (если есть)
- **Domain 3:** (если есть)

**Интерпретация (1-2 предложения):**
Prokka определяет как hypothetical protein, Pfam/HMMER, наоборот, с низким (достоверным) значением evalue определяют домен.

---

## 4) Почему это сомнительно (1-2 гипотезы)

Отметьте подходящее и поясните:

- [ ] **Низкий coverage** (< 70%) — совпал только домен, не весь белок
- [ ] **Паралогия / неоднозначные top hits** — несколько похожих белков с разными функциями
- [ ] **Подозрение на границы CDS** (обрезан/удлинён) — длина сильно отличается от референса
- [X] **"hypothetical", но есть домены** — Prokka не нашла гомологов, но Pfam показал консервативные домены
- [ ] **Другое:** ____________________

**Пояснение (2-3 предложения):** В данном случае низкие значения и pident, и coverage. Prokka не нашла гомологов, но Pfam показал консервативные домены.

---

## 5) Предложение более честной аннотации

- **Было:** (Prokka product) hypothetical protein
- **Предлагаю:** (ваш вариант) hypothetical protein
- **Почему** (1 предложение): доказательства совсем слабые

**Философия честной аннотации:**
- Если **сильное доказательство** (pident >80%, coverage >70%, консервативные домены) → можно назвать конкретную функцию
- Если **умеренное** (pident 60-80%, частичный coverage) → добавить **"putative"** (предполагаемый)
- Если **слабое** (только домен, evalue пограничный) → назвать по домену: *"protein containing ABC transporter domain"*
- Если **совсем слабое** → оставить *"hypothetical protein"* или *"uncharacterized protein"*

**Примеры:**
- ❌ "DNA polymerase III" (если coverage 40%) → ✅ "putative DNA polymerase III subunit alpha"
- ❌ "hypothetical protein" (если есть Pfam PF00005 ABC_tran) → ✅ "putative ABC transporter permease"
- ❌ "ribosomal protein L10" (если pident 55%) → ✅ "protein containing ribosomal L10 domain"

---

## 6) Как бы проверили дальше (1-2 идеи)

Примеры шагов для дополнительной валидации:

1. **Ручной BLAST на NCBI nr** — проверить top 10 hits, посмотреть альтернативные аннотации
2. **Сравнить длину с референсом** — если белок короче/длиннее на >20%, возможна ошибка границ CDS
3. **Посмотреть соседние гены** (операон/синтения) — функционально связанные гены часто рядом
4. **Проверить сборку** — открыть BAM в IGV, убедиться что покрытие равномерное, нет разрывов
5. **Поискать в базах KO/COG/KEGG** — альтернативная функциональная классификация
6. **Phylogenetic analysis** — построить дерево с гомологами, проверить кластеризацию

**Ваши 2 идеи:**

1. Сравнить длину с референсом, т.к. белок короче почти на 50%, и возможна ошибка границ CDS
2. Посмотреть соседние гены

---

## Где найти файлы

```
genome_annotation/
├── outputs/
│   └── run_YYYYMMDD_HHMMSS/      ← Ваша папка с результатами
│       ├── prokka/
│       │   ├── ANNOT.gff          ← Gene ID + Prokka product
│       │   └── ANNOT.tsv          ← Табличный формат
│       ├── diamond/
│       │   └── blastp_results.tsv ← DIAMOND hits (12 колонок)
│       └── hmmer/
│           └── hmmscan_domtblout.txt ← Pfam домены
└── homework/
    └── submissions/$GITHUB_USER/
        └── genes_$GITHUB_USER.txt ← Ваш список генов
```

---

## Как извлечь данные

**Найти вашу папку с результатами:**
```bash
OUTDIR=$(ls -td outputs/run_* | head -1)
echo $OUTDIR
```

**Извлечь Prokka annotation для конкретного гена:**
```bash
# Найти в GFF
grep "ID=ANNOT_06789" $OUTDIR/prokka/ANNOT.gff

# Или в TSV (проще читать)
grep "ANNOT_06789" $OUTDIR/prokka/ANNOT.tsv
```

**Извлечь DIAMOND hit для конкретного гена:**
```bash
# Лучший hit (первая строка)
grep "^ANNOT_06789" $OUTDIR/diamond/blastp_results.tsv | head -1

# Топ-5 hits (для проверки паралогии)
grep "^ANNOT_06789" $OUTDIR/diamond/blastp_results.tsv | head -5
```

**Извлечь Pfam домены для конкретного гена:**
```bash
grep "ANNOT_06789" $OUTDIR/hmmer/hmmscan_domtblout.txt | grep -v "^#"
```

**Посчитать coverage вручную:**
```bash
# coverage = (alignment length) / (query length) × 100%
# Пример: length=180, qlen=200 → coverage = 180/200 * 100 = 90%
```

---

## Пример (для ориентира)

### 0) Gene ID
- **Gene/Protein ID:** ANNOT_06789

### 1) Текущая аннотация Prokka
- **Prokka product:** ABC transporter ATP-binding protein
- **Длина белка:** 245 aa

### 2) DIAMOND evidence
```
ANNOT_06789 WP_003231045.1  68.4  234  74  0  1  234  1  234  3e-89  283  ABC transporter ATP-binding protein [Bacillus subtilis]
```

- **pident:** 68.4%
- **evalue:** 3e-89
- **length / qlen:** 234 / 245 (coverage = 95%)
- **stitle:** ABC transporter ATP-binding protein [Bacillus subtilis]

**Интерпретация:**
Высокий coverage (95%) и низкий evalue (3e-89) поддерживают функцию ABC transporter, но pident 68% умеренный — возможно паралог (много ABC transporters в геноме). Нужно проверить альтернативные hits.

### 3) Pfam/HMMER evidence
- **Domain 1:** ABC_tran (PF00005, e=2e-35)
- **Domain 2:** AAA_21 (PF13304, e=5e-12)

**Интерпретация:**
Оба домена характерны для ABC transporters (ABC_tran = ATP-binding cassette, AAA_21 = ATPase domain). Pfam поддерживает общий класс "ABC transporter", но не конкретный субстрат.

### 4) Почему это сомнительно
- [X] **Паралогия / неоднозначные top hits**
- [ ] Низкий coverage
- [ ] Подозрение на границы CDS
- [ ] "hypothetical", но есть домены
- [ ] Другое

**Пояснение:**
B. subtilis имеет >70 ABC transporters с похожей структурой (ATP-binding domain). pident 68% указывает, что это не ortolog, а скорее паралог. Prokka назвала "ABC transporter ATP-binding protein", но не указала конкретный тип (питательные вещества? антибиотики? ионы?). Без дополнительной информации (operonic context, substrate specificity) нельзя быть уверенным.

### 5) Предложение более честной аннотации
- **Было:** ABC transporter ATP-binding protein
- **Предлагаю:** putative ABC transporter ATP-binding protein
- **Почему:** pident 68% умеренный, высокая вероятность паралогии. Добавление "putative" отражает неопределённость.

### 6) Как бы проверили дальше
1. **Посмотреть соседние гены** — если рядом permease/substrate-binding protein того же ABC transporter, можно уточнить субстрат
2. **Ручной BLAST на nr** — проверить топ-10 hits, посмотреть разнообразие аннотаций (все ли "ABC transporter" или есть конкретные?)

---

## Типичные ошибки (избегайте)

❌ **Копировать Prokka annotation как "честную" без проверки** — Prokka часто переносит аннотацию с первого hit, даже если pident умеренный

❌ **Смотреть только pident, игнорируя coverage** — pident 90% при coverage 30% означает "хорошо совпал маленький кусок", не весь белок

❌ **Не проверять альтернативные hits** — если топ-5 hits имеют разные функции, это признак паралогии

❌ **Предлагать слишком конкретную функцию при низком coverage** — "DNA polymerase III subunit alpha" → лучше "putative DNA polymerase subunit"

❌ **Игнорировать Pfam** — даже если DIAMOND не нашёл гомологов, Pfam домены могут указать на общий класс

❌ **Забывать про "putative"** — если есть хоть малейшие сомнения, добавьте "putative" или "probable"

---

## Связь с реальной практикой

В реальных проектах genome annotation:

1. **Автоматическая аннотация** (Prokka, PGAP, RAST) — быстрая, но часто неточная
2. **Ручная курация** (case investigation) — именно это вы делаете в HW1 Part 2
3. **Community annotation** (RefSeq, UniProtKB) — коллективная проверка и исправление ошибок

Ваша задача — научиться быть критичным к автоматическим аннотациям и обосновывать свои предложения доказательствами.

---

## Полезные ссылки

- **Полное задание:** `docs/homework_01.md`
- **Термины:** `docs/glossary.md`
- **Команды:** `docs/cheatsheet.md`
- **Формат вывода:** `docs/expected_outputs.md`
- **Проблемы:** `docs/troubleshooting.md`
