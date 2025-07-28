# Dojeon Backend

A Spring Boot REST API backend for the Dojeon concert community platform.

## 🚀 Features

- **User Management**: Registration, login, profile management
- **Post System**: Create, read, update, delete posts with likes
- **Comment System**: Add comments to posts
- **Concert Information**: Manage concert data
- **Visitor Tracking**: Track daily visitors
- **CORS Configuration**: Cross-origin resource sharing support
- **Security**: BCrypt password encryption

## 🛠️ Technology Stack

- **Framework**: Spring Boot 3.x
- **Database**: MySQL (AWS RDS)
- **ORM**: JPA/Hibernate
- **Security**: Spring Security with BCrypt
- **Build Tool**: Maven
- **Containerization**: Docker
- **CI/CD**: GitHub Actions

## 📁 Project Structure

```
backend/
├── src/
│   ├── main/
│   │   ├── java/com/dojeon/backend/
│   │   │   ├── controller/          # REST API endpoints
│   │   │   │   ├── UserController.java
│   │   │   │   ├── PostController.java
│   │   │   │   ├── CommentController.java
│   │   │   │   ├── ConcertController.java
│   │   │   │   └── VisitorController.java
│   │   │   ├── service/             # Business logic
│   │   │   │   ├── UserService.java
│   │   │   │   ├── PostService.java
│   │   │   │   ├── CommentService.java
│   │   │   │   ├── ConcertService.java
│   │   │   │   ├── VisitorService.java
│   │   │   │   └── LikeService.java
│   │   │   ├── repository/          # Data access layer
│   │   │   │   ├── UserRepository.java
│   │   │   │   ├── PostRepository.java
│   │   │   │   ├── CommentRepository.java
│   │   │   │   ├── ConcertRepository.java
│   │   │   │   ├── VisitorRepository.java
│   │   │   │   └── LikeRepository.java
│   │   │   ├── model/               # Entity classes
│   │   │   │   ├── User.java
│   │   │   │   ├── Post.java
│   │   │   │   ├── Comment.java
│   │   │   │   ├── Concert.java
│   │   │   │   ├── Visitor.java
│   │   │   │   └── Like.java
│   │   │   ├── config/              # Configuration classes
│   │   │   │   ├── CorsConfig.java
│   │   │   │   └── SecurityConfig.java
│   │   │   └── BackendApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/                        # Test files (empty)
├── .github/workflows/               # CI/CD configuration
│   └── deploy-backend.yml
├── Dockerfile                       # Docker configuration
├── docker-compose.yml               # Local development
├── pom.xml                          # Maven dependencies
└── README.md                        # This file
```

## 🔧 API Endpoints

### User Management
- `POST /api/users/register` - Register new user
- `POST /api/users/login` - User login
- `GET /api/users/check-email` - Check email availability
- `GET /api/users/profile` - Get user profile
- `GET /api/users/statistics` - Get user statistics
- `GET /api/users/activity` - Get user activity
- `PUT /api/users/update-profile` - Update user profile

### Posts
- `GET /api/posts` - Get all posts
- `POST /api/posts` - Create new post
- `GET /api/posts/{id}` - Get specific post
- `PUT /api/posts/{id}` - Update post
- `DELETE /api/posts/{id}` - Delete post
- `GET /api/posts/concert/{concertId}` - Get posts by concert
- `POST /api/posts/{id}/like` - Like/unlike post
- `GET /api/posts/{id}/like/check` - Check like status

### Comments
- `GET /api/comments` - Get all comments
- `POST /api/comments` - Create new comment
- `GET /api/comments/post/{postId}` - Get comments by post
- `PUT /api/comments/{id}` - Update comment
- `DELETE /api/comments/{id}` - Delete comment

### Concerts
- `GET /api/concerts` - Get all concerts
- `POST /api/concerts` - Create new concert
- `GET /api/concerts/{id}` - Get specific concert
- `PUT /api/concerts/{id}` - Update concert
- `DELETE /api/concerts/{id}` - Delete concert

### Visitors
- `POST /api/visitors/record` - Record visitor
- `GET /api/visitors/today` - Get today's visitors

## 🚀 Quick Start

### Prerequisites
- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+
- Docker (optional)

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://github.com/kwohyuno/dojeon-BE.git
   cd dojeon-BE
   ```

2. **Configure database**
   - Update `src/main/resources/application.properties`
   - Set your MySQL connection details

3. **Run with Maven**
   ```bash
   ./mvnw spring-boot:run
   ```

4. **Run with Docker**
   ```bash
   docker-compose up
   ```

### Production Deployment

1. **Build the application**
   ```bash
   ./mvnw clean package -DskipTests
   ```

2. **Build Docker image**
   ```bash
   docker build -t dojeon-backend .
   ```

3. **Run container**
   ```bash
   docker run -d \
     --name dojeon-backend \
     -p 8080:8080 \
     -e SPRING_DATASOURCE_URL=your_db_url \
     -e SPRING_DATASOURCE_USERNAME=your_username \
     -e SPRING_DATASOURCE_PASSWORD=your_password \
     -e CORS_ALLOWED_ORIGINS=your_frontend_url \
     dojeon-backend
   ```

## 🔐 Environment Variables

### Required for Production
- `SPRING_DATASOURCE_URL` - Database connection URL
- `SPRING_DATASOURCE_USERNAME` - Database username
- `SPRING_DATASOURCE_PASSWORD` - Database password
- `SPRING_JPA_HIBERNATE_DDL_AUTO` - JPA DDL mode (update/validate)
- `CORS_ALLOWED_ORIGINS` - Allowed frontend origins (comma-separated)

### Example
```bash
SPRING_DATASOURCE_URL=jdbc:mysql://your-db-host:3306/dojeon
SPRING_DATASOURCE_USERNAME=admin
SPRING_DATASOURCE_PASSWORD=your_password
SPRING_JPA_HIBERNATE_DDL_AUTO=update
CORS_ALLOWED_ORIGINS=http://localhost:3000,http://your-frontend-domain
```

## 🐳 Docker

### Build Image
```bash
docker build -t dojeon-backend .
```

### Run Container
```bash
docker run -d \
  --name dojeon-backend \
  --restart unless-stopped \
  -p 8080:8080 \
  -e SPRING_DATASOURCE_URL=$DB_URL \
  -e SPRING_DATASOURCE_USERNAME=$DB_USERNAME \
  -e SPRING_DATASOURCE_PASSWORD=$DB_PASSWORD \
  -e CORS_ALLOWED_ORIGINS=$CORS_ORIGINS \
  dojeon-backend
```

## 🔄 CI/CD

The project uses GitHub Actions for automated deployment:

1. **Manual Trigger**: Go to Actions → Deploy Backend → Run workflow
2. **Environment**: Select production/staging
3. **Deployment**: Automatically deploys to EC2 instance

### Required GitHub Secrets
- `EC2_HOST` - EC2 instance IP
- `EC2_USERNAME` - SSH username (ec2-user)
- `EC2_SSH_KEY` - SSH private key
- `SPRING_DATASOURCE_URL` - Database URL
- `SPRING_DATASOURCE_USERNAME` - Database username
- `SPRING_DATASOURCE_PASSWORD` - Database password
- `SPRING_JPA_HIBERNATE_DDL_AUTO` - JPA DDL mode
- `CORS_ALLOWED_ORIGINS` - Allowed origins

## 📊 Database Schema

### Users
- `id` (Primary Key)
- `email` (Unique)
- `password` (Encrypted)
- `name`
- `created_at`

### Posts
- `id` (Primary Key)
- `title`
- `content`
- `user_email` (Foreign Key)
- `concert_id` (Foreign Key)
- `like_count`
- `created_at`

### Comments
- `id` (Primary Key)
- `content`
- `user_email` (Foreign Key)
- `post_id` (Foreign Key)
- `created_at`

### Concerts
- `id` (Primary Key)
- `title`
- `artist`
- `venue`
- `date`
- `description`

### Visitors
- `id` (Primary Key)
- `ip_address`
- `visited_at`

### Likes
- `id` (Primary Key)
- `user_email`
- `post_id`
- `created_at`

## 🔧 Configuration

### CORS Configuration
Configured in `CorsConfig.java` to allow cross-origin requests from frontend.

### Security Configuration
- CSRF disabled for API endpoints
- BCrypt password encryption
- All endpoints publicly accessible (for API usage)

### Database Configuration
- MySQL with HikariCP connection pool
- JPA/Hibernate for ORM
- Automatic schema updates

## 🧪 Testing

Currently no test files implemented. Future improvements should include:
- Unit tests for services
- Integration tests for controllers
- Database migration tests

## 📝 API Documentation

The API follows RESTful conventions:
- `GET` for retrieving data
- `POST` for creating new resources
- `PUT` for updating existing resources
- `DELETE` for removing resources

All responses are in JSON format with appropriate HTTP status codes.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is part of the Dojeon concert community platform.

## 🆘 Support

For issues and questions:
- Create an issue in the GitHub repository
- Contact the development team

---

**Last Updated**: December 2024
**Version**: 1.0.0 
