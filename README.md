# HBnB_Part1


## Task 0: High-Level Package Diagram

This diagram represents the three-layer architecture of the HBnB application, organized as follows:

- **Presentation Layer**: This layer handles all user interactions through exposed APIs and services. It serves as the interface between the users (or external systems) and the application's core functionalities. Key components include `ServiceAPI`, `WebUI`, and `RESTAPI`, which allow access to the application's features.

- **Business Logic Layer**: The core of the application resides in this layer, where the business rules and logic are implemented. It includes the primary models, such as `User`, `Place`, `Review`, and `Amenity`, that define the entities in the system. This layer ensures that the data manipulated follows the application's rules.

- **Persistence Layer**: This layer is responsible for managing the connection to the database and performing all storage and retrieval operations. It includes components like `UserRepository`, `PlaceRepository`, and `DatabaseAccess`, which abstract the database operations and allow the Business Logic Layer to interact with the underlying data.

The **Facade Pattern** plays a key role by simplifying communication between these layers. It provides a unified interface that hides the complexities of the Business Logic Layer, allowing the Presentation Layer to interact with it without needing to know its inner workings.


![HBNB UML Task 0](UML/Task0.jpg)


## Task 1: Detailed Class Diagram for Business Logic Layer

In this task, we created a detailed class diagram representing the key entities and relationships within the Business Logic layer of the HBnB application. The diagram focuses on the following core entities: **User**, **Place**, **Review**, and **Amenity**. Each entity is designed with specific attributes and methods to support the application's functionality.

### Key Entities:
- **User**: Represents the individuals using the platform. Each user can create places and write reviews. Attributes include a unique identifier (UUID), name, email, and timestamps for creation and updates.

- **Place**: Represents properties listed on the platform. A place can have multiple reviews and amenities. Attributes include the name, location, capacity, and timestamps for creation and updates. The entity also contains methods for adding amenities and retrieving reviews.

- **Review**: Represents feedback left by users on specific places. Each review includes a rating and text, as well as timestamps. A user can write multiple reviews for different places.

- **Amenity**: Represents the features offered by a place, such as WiFi or a pool. This entity is associated with places through a composition relationship.

### Relationships:
- **User to Place**: A user can create multiple places (one-to-many association).
- **User to Review**: A user can write multiple reviews (one-to-many association).
- **Place to Review**: A place can have multiple reviews (one-to-many association).
- **Place to Amenity**: A place can have multiple amenities (composition relationship), meaning amenities are tightly coupled to places and do not exist independently.

This diagram is essential for understanding the architecture of the business logic layer and the interactions between these core entities.

![HBNB UML Task 1](UML/Task1.png)


## Task 2: Sequence Diagrams for API Calls

The following diagrams illustrate the interactions between the user, the API, the Business Logic, and the database during different operations.

### 1. User Registration
1. **User**: Sends a registration request to the API with their information (name, email, password, etc.).
2. **API**: Receives the request and validates the fields (checks if the email is properly formatted, if the password meets the rules, etc.).
3. **API**: Sends the information to the Business Logic to check if the user already exists and to prepare the creation of the new user.
4. **BusinessLogic**: Checks the uniqueness of the email in the database.
5. **Database**: If the email is unique, the database accepts the user creation request and sends a confirmation.
6. **BusinessLogic**: If the registration is successful, the business logic can create an authentication token or generate a confirmation email.
7. **API**: Sends a response to the user confirming the registration, possibly with an activation link or an access token.

### 2. Place Creation
1. **User**: Sends a place creation request.
2. **API**: Receives the request and sends it to the Business Logic for processing.
3. **BusinessLogic**: Validates the request and sends the information to the database for storage.
4. **Database**: Stores the new place in the database and sends a confirmation to the Business Logic.
5. **BusinessLogic**: Confirms the registration to the API.
6. **API**: Returns a response to the user.

### 3. Review Submission
1. **User**: Sends a review submission request.
2. **API**: Receives the request and sends it to the Business Logic for validation.
3. **BusinessLogic**: Validates the review and stores it in the database.
4. **Database**: Saves the review in the database.
5. **BusinessLogic**: Confirms the registration to the API.
6. **API**: Returns a response to the user.

### 4. Fetching a List of Places
1. **User**: Sends a request to get a list of places.
2. **API**: Sends the request to the Business Logic.
3. **BusinessLogic**: Requests the list of places from the database based on the given criteria.
4. **Database**: Returns the list of places to the Business Logic.
5. **BusinessLogic**: Sends the list of places to the API.
6. **API**: Returns the list of places to the user.

![HBNB UML Task 2 ](UML/Task2.png)
