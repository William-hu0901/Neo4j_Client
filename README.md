# Neo4j Client

This is a Java project for testing Neo4j graph database functionality, providing complete CRUD operations and graph database feature demonstrations.

## Project Features

- **Neo4j Graph Database Support**: Connect to Neo4j database for graph operations
- **Complete CRUD Operations**: Create, Read, Update, Delete nodes and relationships
- **Modern Java**: Built with Java 21 and Maven
- **Comprehensive Testing**: Includes integration tests and unit tests
- **Logging**: Uses SLF4J and Logback for logging
- **Configuration Management**: External configuration via application.properties

## Connection Example

### Neo4j Connection Example
```java
// Configuration
Neo4jConfig config = new Neo4jConfig();
Neo4jConnector connector = new Neo4jConnector(config);

// Initialize database
Neo4jDatabaseInitializer initializer = new Neo4jDatabaseInitializer(connector);
Neo4jMovieService movieService = new Neo4jMovieService(connector);
initializer.initializeDatabase();

// CRUD operations
Movie movie = new Movie("Inception", 2010, "Science Fiction", "A thief enters dreams");
movieService.createMovie(movie);

// Add relationships
movieService.addActor("Inception", "Leonardo DiCaprio");
movieService.addDirector("Inception", "Christopher Nolan");

// Query operations
List<Movie> allMovies = movieService.getAllMovies();
List<Person> actors = movieService.getActorsInMovie("Inception");
List<Movie> actorMovies = movieService.getMoviesByActor("Leonardo DiCaprio");

// Update and delete
Movie updated = new Movie("Inception", 2010, "Thriller", "Updated description");
movieService.updateMovie("Inception", updated);
movieService.deleteMovie("Inception");
```

## Configuration

The application uses `application.properties` for configuration:

```properties
# Neo4j Database Configuration
neo4j.uri=bolt://localhost:7687
neo4j.username=neo4j
neo4j.password=your_password
neo4j.database=neo4j
```

## Requirements

- Java 21
- Neo4j running on localhost:7687 (for integration tests)
- Maven for dependency management

## Project Structure

```
src/main/java/org/daodao/jdbc/
├── Neo4jMainApplication.java           # Main application entry point
├── config/
│   └── Neo4jConfig.java               # Neo4j configuration
├── connectors/
│   └── Neo4jConnector.java            # Neo4j connection handler
├── exceptions/
│   └── PropertyException.java         # Property loading exception
├── model/
│   ├── Movie.java                     # Movie data model
│   └── Person.java                    # Person data model
├── service/
│   ├── Neo4jDatabaseInitializer.java  # Neo4j database initialization
│   └── Neo4jMovieService.java         # Neo4j movie CRUD service
└── util/
    └── Constants.java                  # Application constants

src/test/java/org/daodao/jdbc/neo4j/
├── Neo4jBasicFunctionalityTest.java   # Basic functionality tests
├── Neo4jCRUDTest.java                 # CRUD operations tests
├── Neo4jNewFeaturesTest.java          # Neo4j new features tests
└── Neo4jTestSuite.java                # Test suite
```

## Running the Application

### Using Maven
```bash
mvn compile exec:java -Dexec.mainClass="org.daodao.jdbc.Neo4jMainApplication"
```

## Running Tests

### All Tests
```bash
mvn test
```

### Specific Test Classes
```bash
# Run all Neo4j tests
mvn test -Dtest=Neo4jTestSuite

# Run specific test classes
mvn test -Dtest=Neo4jCRUDTest
mvn test -Dtest=Neo4jBasicFunctionalityTest
mvn test -Dtest=Neo4jNewFeaturesTest
```

## Test Coverage

### Neo4j Tests

**Neo4jCRUDTest**: Basic CRUD operations tests
- Basic node and relationship operations
- Movie and person management
- Database initialization

**Neo4jBasicFunctionalityTest**: Comprehensive basic functionality tests (15+ test cases)
- Node creation and retrieval operations
- Relationship management (ACTED_IN, DIRECTED)
- Graph traversal and path finding
- Data updates and deletions with transaction handling
- Complex Cypher queries with filtering and aggregation

**Neo4jNewFeaturesTest**: Latest Neo4j production features (10+ test cases)
- Multi-database operations and switching
- Advanced Cypher features (subqueries, pattern comprehensions)
- Index and constraint management
- Transaction management with multiple operations
- Performance optimization queries

**Neo4jTestSuite**: Main test suite with comprehensive logging and orchestration
- Coordinated test execution
- Proper setup and cleanup
- Logging and monitoring

**Test Results**: 25+ tests across multiple test classes with high success rate

## Neo4j Features

### Database Features
- Node creation and retrieval operations
- Relationship management (ACTED_IN, DIRECTED)
- Graph traversal and path finding
- Data updates and deletions with transaction handling
- Complex Cypher queries with filtering and aggregation
- Index and constraint management
- Graph database initialization with sample data
- Advanced Cypher features (subqueries, pattern comprehensions)
- Multi-database operations and switching

### Application Features
- Simple CRUD operations
- Custom exception handling
- SLF4J and Logback logging
- Automatic database initialization
- Java21 compatibility
- Comprehensive test coverage
- Parallel compilation support

## Troubleshooting

### Common Issues

1. **Neo4j Connection Failed**
   - Ensure Neo4j is running on localhost:7687
   - Verify credentials in application.properties
   - Check database name configuration

2. **Test Failures**
   - Verify database is running
   - Check connection parameters
   - Ensure correct configuration in application.properties

3. **Maven Build Issues**
   - Ensure Java21 is properly installed
   - Check Maven version compatibility (3.6+)
   - Verify toolchain configuration

### Verification Commands

```bash
# Check Java version
java -version

# Check Maven version
mvn -version

# Test compilation
mvn compile

# Run specific test
mvn test -Dtest=Neo4jTestSuite
```

## License

This project is for educational and demonstration purposes.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request