# Notes

## & &mut
`&` `&mut` - **NU** returneaza RAW pointer, ci **REFERINTE**;  

`&mut`
* Singura **REFERINTA** care **DATELE** care **POINTEAZA**;
* Doar 1 **REFERINTA**;
* **MODIFY SAFE**;

> & != &mut 
* & - >1 REFERINTE catre DATA;

## Tuples
> **GRUPEAZA** mai multe DT de tipuri **DIFERITE**;

### Creare TUPLE
```rust
let persona_cu_type : (&str,i32,f64) = ("Tony", 27, 3,5);
let persona_fara_type = ("Tony", 27, 3.5); 

```
### Decompresarea unui tuplu
```rust
let persoana_cu_type : (&str,i32,f64) = ("Tony",3,3,5);
let (nume, varsta, inaltime) = persoana_cu_type;
```

### Mutabilitatea
```rust
    // Mutabilitate
    let persoana_imutabila = ("Imutabil", 1, 1.0);
    // persoana_imutabila.1 = 1;  cannot mutate
    let mut persoana_mutabila = ("Mutabil", 1, 3.5);
    println!("Inainte DE SCHIMBARE: {:?}", persoana_mutabila);
    persoana_mutabila.0 = "Am schimbat";
    println!("Dupa SCHIMBARE: {:?}", persoana_mutabila);
```

### Ownership

* `i32`, `integer` - implementeaza `trait COPY`, astfel **valoarea este COPIATA**;
* `String` - **NU** implementeaza `trait COPY` , astfel **valoarea este MUTATA**;
```rust
    // Proprietatea
    let tuplu_copy = (42, "Tuplu Text".to_string()); 
    println!("tuplu_copy: {:?}",tuplu_copy);
    // # i32 implementeaza trasatura COPY;
    // # String NU implementeaza COPY, asa ca-l MUTA in "text"
    let (nr, text) = tuplu_copy;
    println!("Nr copiat in tuplu - nr :  {}", tuplu_copy.0); 
    // print!("tuplu_copy.1 : {}", tuplu_copy.1); # String nu implementeaza trasatura COPY;
    println!("tup.1 este mutat in text: {}", text);
```

### Tuplu ca si parametrul unei functii

```rust
    /*  
        * IF ALL elementele tuplului implementeaza COPY => tuplul poate fi copiat;
        * IF ALL elementele tuplului implementeaza COPY => NU va TRASNFERA OWNERSHIP atunci este pasat unui functii FARA a folosii 1 REFERINTA;
********************************************************************************************************
        * IF pasezi o REF catre tuplu, atunci NU TRANSFERA OWNERSHIP; 
        * IF >=1 element in tuplu este NON-COPY, OWNERSHIP este transferat atunci cand este pasat unei functii FARA a folosii o REFERINTA;
    */

    /*
        IF tuplu_non-COPY-> fn x(tuplu: &(i32, String)) -> x(&tuplu_non-COPY)
        IF tuplu_COPY - > fn y(tuplu: (i32, i32)) -> y(tuplu_COPY);

     */
    // NON-COPY
    let tuplu_non_copy : (i32,String)= (10, "NOT COPY".to_string());
    afiseaza_referinte_tuplu(&tuplu_non_copy); // PRIMESTE 1 REFERINTA;

    fn afiseaza_referinte_tuplu(tuplu: &(i32,String)) { //VA primi 1 REFERINTA;
        println!("Afiseaza referinte tuplu: {}, {}", tuplu.0, tuplu.1);
    }

    // COPY
    let tuplu_copy:(i32,i32) = (10,50); 
    fn afiseaza_copy_tuplu (tuplu:(i32,i32)){
        println!("Afiseaza COPY TUPLU: {} {}", tuplu.0, tuplu.1);
    }
    afiseaza_copy_tuplu(tuplu_copy); // VA PRIMI 1 COPIE; APEL FARA REFERINTA;

    // OWNERSHIP DE LA NON-COPY cu apel FARA REFERINTA
    fn afiseaza_tuplu_ownership(tuplu_non: (i32, String)){
        println!("Afiseaza OWNERSHIP Tuplu NON-COPY cu apel fara REF: {} {}", tuplu_non.0, tuplu_non.1);
    }
    afiseaza_tuplu_ownership(tuplu_non_copy);


```
