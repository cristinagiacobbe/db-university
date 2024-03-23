Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## DEVO ANCORA INDICARE IL TIPO DI GRANDEZZA DI CIASCUN DATO DELLE TABELLE

# DB Schema

## Departments
- Id
- Name
- Nation
- City
- Cap
- Address
- Sector (umanistic, sanitary, ing., ...)
- Property (public/private)
- Access (free, limited access)
- Training method (telematic, traditional)
- Rector

## Degree courses (Degree-course)
- Id
- Name (denominazione)
- Department of belonging_id
- Years duration
- Didactic centre (sede)
- President

## Courses (Course)
- Id
- Degree coure of belonging_id
- Start course (date)
- Main handbook
- Segretery email

## Teachers (Teacher)
- Id
- Name
- Lastname
- Course_id
- Level (assistente, associato, ordinario)


## Exam sessions (Exam-session)
- Id
- Course_id
- Date
- Place
- Email for sign up

## Students (student)
- Id
- Name
- Lastname
- Date of birth
- Address
- Degree course_id
- Email

## Examinations (Examination)
- Id
- Date
- Vote
- Course_id
- Student_id
