<!-- 
Modellare la struttura di un database per memorizzare tutti i dati riguardanti una università:

sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;

per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella. 
-->


## Table name:
- departments
- cources_of_degree
- courses
- teachers
- exams
- students
- student_exams

## Tables:

### Departments
- id | BIGINT - AUTO_INCREMENT - PRIMARY KEY
- name | VARCHAR(200) - NOT NULL
- website
- phone
- email


### Courses of Degree (one to many => departments)
- id | BIGINT - AUTO_INCREMENT - PRIMARY KEY
- department_id | FOREIGN KEY
- name | VARCHAR(200) - NOT NULL
- description | TEXT
- period | VARCHAR(200) - NOT NULL


### Courses (many to many => teachers)
- id | BIGINT - AUTO_INCREMENT - PRIMARY KEY
- course_of_degree_id | FOREIGN KEY
- name | VARCHAR(200) - NOT NULL
- description | TEXT


## Pivot: course teacher
- course_id | FOREIGN KEY
- teacher_id | FOREIGN KEY


### Teachers
- id | BIGINT - AUTO_INCREMENT - PRIMARY KEY
- first_name | VARCHAR(100) - NOT NULL
- last_name | VARCHAR(100) - NOT NULL
- email | VARCHAR(100) - NOT NULL - UNIQUE
- phone_number | VARCHAR(20) - NOT NULL


### Exams
- id | BIGINT - AUTO_INCREMENT - PRIMARY KEY
- course_id | FOREIGN KEY
- date | DATE - NOT NULL
- hour | TIME - NOT NULL


## Pivot: students exams
- student_id
- exam_id
- vote | TINYINT(2) - NOT NULL


### Students (one to many => cources_of_degree)
- id | BIGINT - AUTO_INCREMENT - PRIMARY KEY
- course_of_degree_id | FOREIGN KEY
- first_name | VARCHAR(100) - NOT NULL
- last_name | VARCHAR(100) - NOT NULL
- email | VARCHAR(100) - NOT NULL - UNIQUE
- phone_number | VARCHAR(20) - NOT NULL
- registration_number | VARCHAR(20) - NOT NULL - UNIQUE



