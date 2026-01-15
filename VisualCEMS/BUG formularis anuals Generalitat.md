Cal tenir en compte, en el moment d’anomenar els fitxers PDF, que el nom ha de contenir el nom del _foco_ **sense separadors**, per exemple: `INDULLEIDAIL`.
És a dir, si el nom del _foco_ és `pv22_indulleida_il`, el valor que s’ha d’indicar al fitxer `config1.xml` ha de ser `INDULLEIDAIL`, `INDULLEIDA o bé IL`.

**ATENCIÓ:** si s’utilitza `INDULLEIDA_IL` com a nom, l’informe fallarà. Això és degut al fet que el caràcter `_` s’utilitza com a separador durant el procés de _generació_ dels informes.


Per tant, al fitxer de configuració `config1.xml` el nom del _foco_ ha de ser `INDULLEIDAIL`, i els fitxers PDF han de tenir els noms següents:
- `INDULLEIDAIL_especific_focus.pdf`
- `INDULLEIDAIL_especific_establiment.pdf`

![[Pasted image 20251215120428.png]]