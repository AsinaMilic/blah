# NephroInnovate API - Django with MongoDB!!!

A Django implementation of the NephroInnovate API with MongoDB integration.

## Features

- Django REST Framework with MongoDB integration through Djongo
- User authentication with JWT tokens
- FHIR-compliant API for healthcare data (Patient, Encounter, Observation, Organization)
- Additional models for Posts
- Comprehensive API documentation (Swagger UI, ReDoc, Markdown guides)
- MongoDB Atlas cloud database integration (configurable)
- Health check endpoints

## FHIR Compliance

This API is fully compliant with the FHIR R4 standard for the following resources:

- Patient
- Organization
- Encounter (specifically for Hemodialysis Sessions)
- Observation (for Laboratory Results and clinical measurements)

For detailed information on FHIR implementation, see:

- [FHIR API Documentation](FHIR_API_DOCUMENTATION.md)
- [FHIR API Quick Reference](FHIR_QUICK_REFERENCE.md)
- [FHIR API Developer Guide](FHIR_DEVELOPER_GUIDE.md)

## Getting Started

### Prerequisites

- Python 3.8+
- MongoDB (local or Atlas)
- Java (for FHIR validator, optional for development)

### Installation

1. Clone the repository

```bash
git clone https://github.com/yourusername/nephroinnovate-api-django.git
cd nephroinnovate-api-django
```

2. Create and activate a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows, use: venv\Scripts\activate
```

3. Install dependencies

```bash
pip install -r requirements.txt
```

4. Create a `.env` file based on `.env.example`

```bash
cp .env.example .env
```

5. Update the `.env` file with your configuration:

    - `MONGO_DATABASE_NAME`
    - `MONGO_USERNAME`
    - `MONGO_PASSWORD`
    - `MONGO_HOST` (e.g., `localhost:27017` or your Atlas cluster URI)
    - `SECRET_KEY` (generate a new strong secret key)

6. Run migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

7. Create a superuser

```bash
python manage.py createsuperuser
```

8. Run the development server

```bash
python manage.py runserver
```

The API will be available at http://localhost:8000/.

## API Documentation

Once the server is running, you can access the API documentation at:

- Swagger UI: http://localhost:8000/documentation/
- ReDoc: http://localhost:8000/redoc/
- Markdown Guides:
    - [FHIR API Documentation](FHIR_API_DOCUMENTATION.md)
    - [FHIR API Quick Reference](FHIR_QUICK_REFERENCE.md)
    - [FHIR API Developer Guide](FHIR_DEVELOPER_GUIDE.md)

## Project Structure

- `core/` - Core utilities, base models, FHIR validation setup
- `users/` - User authentication and management
- `patients/` - FHIR Patient resource implementation
- `organizations/` - FHIR Organization resource implementation
- `laboratory/` - FHIR Encounter and Observation resources for hemodialysis and lab results
- `posts/` - Simple blog/article functionality
- `health/` - Health check endpoints
- `tests/` - Unit and integration tests, including FHIR compliance tests
- `nephroinnovate/` - Django project settings and main URL configuration

## MongoDB Collections

This project uses MongoDB for data storage via Djongo. Key collections include:

- `users_user`
- `users_usersettings`
- `patients_patient`
- `organizations_organization`
- `laboratory_hemodialysissession` (maps to FHIR Encounter)
- `laboratory_laboratoryresult` (maps to FHIR Observation)
- `posts_post`

## Running FHIR Compliance Tests

To ensure ongoing FHIR compliance, you can run the dedicated test suite:

```bash
python manage.py test tests.test_fhir_compliance -v 2
```

This requires the HL7 FHIR Validator JAR (`validator_cli.jar`) to be present in the project root.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
