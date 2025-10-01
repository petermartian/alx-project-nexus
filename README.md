# Project Nexus Documentation

Welcome to **Project Nexus**, a GitHub repository dedicated to documenting key learnings from the **ProDev Backend Engineering** program. This repository serves as a knowledge hub, showcasing my understanding of backend engineering concepts, tools, and best practices acquired throughout the program. It is designed to be a reference for current and future learners and to foster collaboration between frontend and backend developers.

## Project Objective

The goal of **Project Nexus** is to:
- Consolidate and document major learnings from the ProDev Backend Engineering program.
- Provide detailed explanations of backend technologies, concepts, challenges, and solutions.
- Serve as a reference guide for learners and developers.
- Encourage collaboration between frontend and backend learners to build cohesive projects.

## Overview of ProDev Backend Engineering Program

The **ProDev Backend Engineering** program is an intensive course focused on equipping learners with the skills to design, develop, and deploy robust backend systems. The program covers a wide range of modern backend technologies, tools, and best practices, emphasizing hands-on projects and real-world problem-solving. Key areas of focus include:

- **Core Technologies**: Python, Django, REST APIs, GraphQL, Docker, and CI/CD pipelines.
- **Development Concepts**: Database design, asynchronous programming, caching strategies, and system design.
- **Practical Application**: Building scalable APIs, integrating message queues (e.g., Celery with RabbitMQ), and deploying applications to production environments like Render.
- **Collaboration**: Working with frontend learners to integrate backend APIs with user interfaces.

The program emphasizes not only technical skills but also collaboration, problem-solving, and adherence to industry best practices.

## Major Learnings

### Key Technologies Covered

1. **Python**: The backbone of backend development in the program, used for its simplicity and versatility in building scalable applications.
2. **Django**: A high-level Python web framework used to create secure and maintainable RESTful APIs, as demonstrated in my ALX Travel App project.
3. **REST APIs**: Designed and implemented RESTful endpoints for CRUD operations, integrated with frontend applications.
4. **GraphQL**: Explored as an alternative to REST, offering flexible querying for complex data structures.
5. **Docker**: Utilized for containerizing applications to ensure consistent development and deployment environments.
6. **CI/CD**: Implemented continuous integration and deployment pipelines using GitHub Actions and Render for automated testing and deployment.
7. **Celery & RabbitMQ**: Used for asynchronous task processing, such as handling payment verifications in the ALX Travel App.
8. **Redis**: Employed as a caching layer and message broker for Celery tasks.

### Important Backend Development Concepts

1. **Database Design**:
   - Designed relational databases using PostgreSQL (via `dj_database_url`) for efficient data storage and retrieval.
   - Applied normalization principles to minimize redundancy and ensure data integrity.
   - Example: In the ALX Travel App, created models for listings and payments with proper relationships (e.g., ForeignKey for user associations).

2. **Asynchronous Programming**:
   - Leveraged Celery with RabbitMQ/Redis to handle time-consuming tasks like payment processing and email notifications.
   - Ensured non-blocking operations to improve user experience and application performance.

3. **Caching Strategies**:
   - Explored Redis for caching frequently accessed data to reduce database load.
   - Planned implementation of caching for API responses in high-traffic endpoints (e.g., listing searches).

4. **System Design**:
   - Learned to design scalable systems with components like load balancers, microservices, and message queues.
   - Applied principles in the ALX Travel App by separating concerns (e.g., payment processing via Chapa, geolocation via `django-ip-geolocation`).

### Challenges Faced and Solutions Implemented

#### Challenge 1: IP Geolocation Error in Django Application
- **Issue**: During deployment of the ALX Travel App on Render, the `django-ip-geolocation` middleware raised an `AttributeError` and `ImportError` due to an incorrect backend configuration (`django_ip_geolocation.backends.ipapi` was specified, but this backend does not exist in the package).
- **Logs**:
- ## Challenges and Solutions

This section documents some of the real-world challenges faced during the projects and the solutions that were implemented.

### 1. Incorrect Django Project Structure
* **Problem**: Projects frequently had a tangled file structure, often missing the main `manage.py` file at the root. This caused `manage.py: No such file or directory` errors when trying to run server commands.
* **Solution**: The issue was resolved by using the `django-admin startproject <name> .` command to generate the standard project layout. We then used terminal commands (`mv`, `rm`) to move existing app files into their correct locations and delete duplicates, restoring a clean and predictable structure.

### 2. `ModuleNotFoundError` During Deployment
* **Problem**: A successfully running local application would fail during deployment on Render with errors like `ModuleNotFoundError: No module named 'alx_travel_app.settings'`.
* **Solution**: This was a naming mismatch. The root cause was that the name of the project's configuration folder did not match the import path used in configuration files (`settings.py`, `wsgi.py`). The fix involved identifying the folder's true name and updating all configuration strings to use that correct name.

### 3. `ImportError` Due to Model Naming Inconsistency
* **Problem**: The application would crash with `ImportError: cannot import name 'Listing' from 'listings.models'`, even though the database model was clearly defined.
* **Solution**: We discovered the model was named **`Hotel`** in `models.py`, but every other file (`views.py`, `admin.py`, `serializers.py`) was trying to import and use **`Listing`**. The solution was a systematic refactor, replacing every incorrect reference to `Listing` with the correct model name, `Hotel`.

### 4. `DisallowedHost` Error on Live Server
* **Problem**: After deploying, accessing the public Render URL resulted in a Django `DisallowedHost` error page, blocking all requests.
* **Solution**: As a Django security feature, `ALLOWED_HOSTS` must be configured in production. We fixed this by updating `settings.py` to read Render's built-in `RENDER_EXTERNAL_HOSTNAME` environment variable and dynamically add it to the `ALLOWED_HOSTS` list, making the solution portable and secure.

### 5. Package and Configuration Typos
* **Problem**: Builds would fail during the `pip install` step due to a typo in `requirements.txt` (`corsheaders` instead of `django-cors-headers`). A similar issue occurred with an incorrect configuration path for the `django-ip-geolocation` library.
* **Solution**: The fix was to carefully read the error logs to identify the typo and correct the package name. For the library configuration, we updated the path in `settings.py` to point to the specific class (`...ipapi.Ipapi`) instead of just the module, as required by the library's documentation.
