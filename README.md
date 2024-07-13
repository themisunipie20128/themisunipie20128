# YpoxreotikiErgasia24_<AM>_<Epwnymo>_<Onoma>

## Περιεχόμενα
1. [Επιπλέων Παραδοχές που Επιλέξατε](#επιπλέων-παραδοχές-που-επιλέξατε)
2. [Τεχνολογίες που Χρησιμοποιήθηκαν](#τεχνολογίες-που-χρησιμοποιήθηκαν)
3. [Περιγραφή των Αρχείων που Κατασκευάσατε](#περιγραφή-των-αρχείων-που-κατασκευάσατε)
4. [Τρόπος Εκτέλεσης Συστήματος](#τρόπος-εκτέλεσης-συστήματος)
5. [Τρόπος Χρήσης του Συστήματος](#τρόπος-χρήσης-του-συστήματος)
    - [Είσοδος ως Διαχειριστής](#είσοδος-ως-διαχειριστής)
    - [Δημιουργία Ιατρού](#δημιουργία-ιατρού)
    - [Δημιουργία Ασθενή](#δημιουργία-ασθενή)
    - [Κράτηση Ραντεβού](#κράτηση-ραντεβού)
    - [Προβολή Ραντεβού Ιατρού](#προβολή-ραντεβού-ιατρού)
6. [Αναφορές που Χρησιμοποιήσατε](#αναφορές-που-χρησιμοποιήσατε)

## Επιπλέων Παραδοχές που Επιλέξατε
1. Κάθε ραντεβού διαρκεί μία ώρα και δεσμεύεται μία ώρα από το ωράριο του ιατρού.
2. Το σύστημα επιτρέπει τη δημιουργία, τροποποίηση και διαγραφή λογαριασμών ιατρών και ασθενών μόνο από τον διαχειριστή.
3. Οι ασθενείς μπορούν να κάνουν κράτηση ραντεβού μόνο σε διαθέσιμες ώρες των ιατρών.
4. Οι ειδικότητες των ιατρών είναι προεπιλεγμένες και συγκεκριμένες: Ακτινολόγος, Αιματολόγος, Αλλεργιολόγος, Παθολόγος και Καρδιολόγος.

## Τεχνολογίες που Χρησιμοποιήθηκαν
- Python 3.8
- Flask
- Flask-Bcrypt
- Flask-JWT-Extended
- PyMongo
- Werkzeug
- MongoDB
- Docker
- Docker Compose

## Περιγραφή των Αρχείων που Κατασκευάσατε

### `app.py`
Αυτό το αρχείο περιέχει την κύρια εφαρμογή Flask και τις αρχικοποιήσεις για το Bcrypt, JWTManager και MongoDB client.

### `wsgi.py`
Αυτό το αρχείο περιέχει το entry point για την εφαρμογή όταν εκτελείται σε περιβάλλον WSGI.

### `routes.py`
Αυτό το αρχείο περιέχει τα routes της εφαρμογής για τις λειτουργίες των διαχειριστών, ιατρών και ασθενών.

### `requirements.txt`
Περιέχει όλες τις απαιτούμενες βιβλιοθήκες για την εφαρμογή.

### `Dockerfile`
Περιγράφει την κατασκευή του Docker image για την εφαρμογή.

### `docker-compose.yml`
Περιέχει τις ρυθμίσεις για την εκτέλεση των containers για την εφαρμογή και τη βάση δεδομένων MongoDB.

### `.env`
Περιέχει τις μεταβλητές περιβάλλοντος για την εφαρμογή.

## Τρόπος Εκτέλεσης Συστήματος

### Προαπαιτούμενα
- Εγκατάσταση Docker και Docker Compose

### Βήματα Εκτέλεσης
1. Κλωνάρετε το repository:
    ```bash
    git clone https://github.com/<username>/YpoxreotikiErgasia24_<AM>_<Epwnymo>_<Onoma>.git
    cd YpoxreotikiErgasia24_<AM>_<Epwnymo>_<Onoma>
    ```

2. Δημιουργήστε το Docker image:
    ```bash
    docker build -t hospital-management-system .
    ```

3. Τρέξτε τα containers με Docker Compose:
    ```bash
    docker-compose up
    ```

4. Η εφαρμογή θα είναι διαθέσιμη στο `http://localhost:5000`.

## Τρόπος Χρήσης του Συστήματος

### Είσοδος ως Διαχειριστής
- URL: `POST /admin/login`
- Σώμα Αιτήματος:
    ```json
    {
        "username": "admin",
        "password": "@dm1n"
    }
    ```

### Δημιουργία Ιατρού
- URL: `POST /admin/doctor`
- Σώμα Αιτήματος:
    ```json
    {
        "first_name": "John",
        "last_name": "Doe",
        "email": "john.doe@example.com",
        "username": "jdoe",
        "password": "password123",
        "specialization": "Cardiologist",
        "appointment_cost": 100
    }
    ```
- Απαιτείται JWT token στο Header: `Authorization: Bearer <JWT_TOKEN>`

### Δημιουργία Ασθενή
- URL: `POST /patient/register`
- Σώμα Αιτήματος:
    ```json
    {
        "first_name": "Jane",
        "last_name": "Doe",
        "email": "jane.doe@example.com",
        "username": "jadoe",
        "password": "password123",
        "amka": "1234567890",
        "birth_date": "1990-01-01"
    }
    ```

### Κράτηση Ραντεβού
- URL: `POST /patient/appointments`
- Σώμα Αιτήματος:
    ```json
    {
        "doctor_username": "jdoe",
        "date": "2024-07-14",
        "time": "10:00",
        "reason": "Checkup",
        "appointment_cost": 100
    }
    ```
- Απαιτείται JWT token στο Header: `Authorization: Bearer <JWT_TOKEN>`

### Προβολή Ραντεβού Ιατρού
- URL: `GET /doctor/appointments`
- Απαιτείται JWT token στο Header: `Authorization: Bearer <JWT_TOKEN>`

## Αναφορές που Χρησιμοποιήσατε
1. [Flask Documentation](https://flask.palletsprojects.com/en/2.0.x/)
2. [Docker Documentation](https://docs.docker.com/)
3. [MongoDB Documentation](https://docs.mongodb.com/)
4. [Flask-JWT-Extended Documentation](https://flask-jwt-extended.readthedocs.io/en/stable/)

