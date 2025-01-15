
# SQL Otázky a Odpovědi

## 1. Upravte tabulku „ucitele“ sloupec „jmeno“ u učitele, který má hodnotu ve sloupci „jmeno“ „Hrdina“, na hodnotu „Zdenek“.
```sql
UPDATE ucitele
SET jmeno = 'Zdenek'
WHERE jmeno = 'Hrdina';
```

---

## 2. Vypište počet žáků ve třídách. Zobrazte sloupec název třídy, počet žáků (tento sloupec bude přesně takto pojmenovaný). Výsledek seřaďte podle názvu třídy podle abecedy.
```sql
SELECT t.nazev AS 'název třídy', COUNT(z.id) AS 'počet žáků'
FROM sis_tridy t
LEFT JOIN sis_zaci z ON t.id = z.trida
GROUP BY t.nazev
ORDER BY t.nazev ASC;
```

---

## 3. Napište dotaz, vypíše jména a příjmení všech žáků, kteří nastoupili do školy v roce 2021. Výsledek bude seřazen podle abecedy podle příjmení, v případě shodného příjmení podle křestního jména. Prefix do dotazu nepište.
```sql
SELECT z.jmeno, z.prijmeni
FROM sis_zaci z
JOIN sis_tridy t ON z.trida = t.id
WHERE t.nastup = 2021
ORDER BY z.prijmeni ASC, z.jmeno ASC;
```

---

## 4. Napište kus dotazu, kde chceme zobrazit produkty, které ve sloupci cena mají hodnotu v rozmezí 1000–2000 (včetně krajních hodnot).
```sql
SELECT *
FROM produkty
WHERE cena BETWEEN 1000 AND 2000;
```

---

## 5. Napište kus kódu podmínky, kde budeme chtít zobrazit všechny výsledky pro ty zákazníky, jejich hodnota ve sloupci customer_id je 2 a 5.
```sql
WHERE customer_id IN (2, 5);
```

---

## 6. Jaký je rozdíl, když v datovém typu nastavím utf8_bin a utf8_czech?
- **`utf8_bin`**: Rozlišuje velká a malá písmena, porovnávání je striktně podle binární reprezentace znaků.
- **`utf8_czech`**: Je přizpůsoben pro český jazyk, bere ohled na diakritiku a řadí podle českých pravidel.

---

## 7. K čemu slouží v jazyku SQL klíčové slovo ORDER BY?
- Slouží k řazení výsledků dotazu podle zvoleného sloupce. Výchozí řazení je vzestupné (`ASC`), nebo lze použít sestupné (`DESC`).

---

## 8. Jak se zapíše podmínka pro tabulku obcí, pokud chceme, aby název obce začínal písmenem H?
```sql
WHERE nazev_obce LIKE 'H%';
```

---

## 9. Co to je dotaz s agregační funkcí? Jaké znáte agregační funkce a k čemu slouží?
- Dotaz s agregační funkcí zpracovává více řádků a vrací jednu hodnotu.
- Příklady agregačních funkcí: 
  - `COUNT`: Počet záznamů.
  - `SUM`: Součet hodnot.
  - `AVG`: Průměr hodnot.
  - `MAX`: Nejvyšší hodnota.
  - `MIN`: Nejnižší hodnota.

---

## 10. K čemu slouží klíčové slovo DISTINCT?
- Slouží k odstranění duplicitních záznamů z výsledků dotazu.

---

## 11. K čemu slouží klíčové slovo HAVING?
- Používá se pro filtrování výsledků agregačních funkcí.
- Například:
```sql
SELECT obor, COUNT(*)
FROM studenti
GROUP BY obor
HAVING COUNT(*) > 5;
```

---

## 12. Uveďte klíčová slova pro vkládání, editaci a mazání.
- **Vkládání**: `INSERT`
- **Editace**: `UPDATE`
- **Mazání**: `DELETE`

---

## 13. Napište část dotazu od FROM dále, tak aby mně to vypsalo všechny učitele, ať už jsou třídní nebo ne a u třídních třídu.
```sql
FROM sis_ucitele u
LEFT JOIN sis_tridy t ON u.id = t.tridni;
```

---

## 14. K čemu slouží aliasy u sloupců nebo u tabulek?
- Alias slouží k přejmenování sloupců nebo tabulek pro zjednodušení a zlepšení čitelnosti dotazů. 
- Například při práci s více tabulkami se stejnými názvy sloupců nebo při složitých výpočtech.

---

## 15. Co znamená zkratka DDL?
- **DDL** znamená **Data Definition Language** (jazyk pro definici dat).
- Používá se pro vytváření, změnu a mazání struktur databáze (např. tabulky, schémata).

---

## 16. Co znamená zkratka DML?
- **DML** znamená **Data Manipulation Language** (jazyk pro manipulaci s daty).
- Slouží k manipulaci s daty v tabulkách, tj. pro vkládání, aktualizaci, mazání nebo čtení dat.
- Příkazy DML zahrnují:
  - `SELECT` – Pro čtení dat.
  - `INSERT` – Pro vkládání dat.
  - `UPDATE` – Pro aktualizaci existujících dat.
  - `DELETE` – Pro mazání dat.

---

## 17. Co znamená zkratka DCL?
- **DCL** znamená **Data Control Language** (jazyk pro řízení dat).
- Slouží ke správě oprávnění a přístupových práv k databázi.
- Příkazy DCL zahrnují:
  - `GRANT` – Udělení oprávnění uživatelům (např. právo na čtení nebo změnu dat).
  - `REVOKE` – Odebrání oprávnění od uživatelů.
