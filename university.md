## Dipartimenti

id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
tipologia (VARCHAR(30), NOTNULL, UNIQUE)
sede (VARCHAR(150), NULL)


## corsi di laurea

id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
id_department (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
tipologia_corso (VARCHAR(50), NOTNULL, UNIQUE)
cfu (SMALLINT, NULL)
numero_iscritti (MEDIUMINT, NULL)

## corsi

id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
id_corso_di_laurea (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
nome_corso (VARCHAR(50), NOTNULL, UNIQUE)
cfu (SMALLINT, NULL)
numero_iscritti (MEDIUMINT, NULL)
aula (VARCHAR(35))


## insegnanti

id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
nome_cognome (VARCHAR(50), NOTNULL)
email (VARCHAR(50), NULL)

## esami 
id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
name (VARCHAR(50), NOTNULL, UNIQUE)
modalità_esame (VARCHAR(10), NULL)

## studenti

id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
nome_cognome (VARCHAR(50), NOTNULL)
email (VARCHAR(50), NULL)
matricola (TINYINT, NOTNULL, UNIQUE)

## votes
id (BIGINT, NOTNULL, UNIQUE, AUTOINCREMENT, PRIMARYKEY)
id_studenti FK
id_esami FK
esito (TINYINT, NULL)
voto(VARCHAR(15), NULL)

## relationship

dipartimento - corsi di laurea -- ONE TO MANY/
corso di laurea - corsi -- ONE TO MANY/
corsi - insegnanti -- MANY TO MANY/
corso di laurea - studenti -- ONE TO MANY/
esami - studenti -- MANY TO MANY
corsi - esami -- ONE TO MANY



Esami                               esami_studenti                 Studenti
id, nome, anno               id,id_studente,id_esame                      id, nome, 
1,  Matematica 1, 2022        1, 1, 1                                         1, Paolo
2,  Matematica 2, 2023        2, 1, 2                                          2, Marco, 