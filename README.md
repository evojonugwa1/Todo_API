# Todo API Documentation

## Product Description

The Todo API is a RESTful web service built with Node.js and Express.js that provides comprehensive task management functionality. This API allows users to create, read, update, and delete todo items, making it perfect for building todo applications, task managers, or integrating task functionality into existing applications.

### Key Features

- **Full CRUD Operations**: Create, read, update, and delete todo items
- **RESTful Design**: Follows REST API conventions for intuitive usage
- **JSON Responses**: All responses are in JSON format for easy integration
- **Lightweight**: Built with minimal dependencies for optimal performance
- **Flexible**: Can be easily extended with additional features
- **Cross-Platform**: Runs on any platform that supports Node.js

### Use Cases

- Personal task management applications
- Team collaboration tools
- Project management systems
- Mobile app backends
- Integration with existing business applications
- Learning RESTful API development

## Getting Started

### Prerequisites

- Node.js (version 14.0 or higher)
- npm (Node Package Manager)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/evojonugwa1/Todo_API.git
   cd Todo_API
   ```

2. **Install dependencies:**
   ```bash
   npm install
   npm install express
   ```

3. **Start the server:**
   ```bash
   node server.js
   ```

4. **Verify installation:**
   The server should start on `http://localhost:3000` (or your configured port)

## API Reference

### Base URL
```
http://localhost:3000/api
```

### Data Model

**Todo Object Structure:**
```json
{
  "id": "string|number",
  "title": "string",
  "description": "string",
  "completed": "boolean",
  "createdAt": "ISO 8601 datetime string",
  "updatedAt": "ISO 8601 datetime string"
}
```

### Endpoints

#### Get All Todos
```http
GET /api/todos
```

**Description:** Retrieve all todo items

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "title": "Complete project documentation",
      "description": "Write comprehensive API documentation",
      "completed": false,
      "createdAt": "2025-06-26T10:00:00.000Z",
      "updatedAt": "2025-06-26T10:00:00.000Z"
    }
  ],
  "count": 1
}
```

#### Get Todo by ID
```http
GET /api/todos/:id
```

**Parameters:**
- `id` (required): Todo item ID

**Response:**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "title": "Complete project documentation",
    "description": "Write comprehensive API documentation",
    "completed": false,
    "createdAt": "2025-06-26T10:00:00.000Z",
    "updatedAt": "2025-06-26T10:00:00.000Z"
  }
}
```

#### Create New Todo
```http
POST /api/todos
```

**Request Body:**
```json
{
  "title": "string (required)",
  "description": "string (optional)",
  "completed": "boolean (optional, defaults to false)"
}
```

**Example Request:**
```json
{
  "title": "Buy groceries",
  "description": "Milk, bread, eggs, and fruits",
  "completed": false
}
```

**Response:**
```json
{
  "success": true,
  "message": "Todo created successfully",
  "data": {
    "id": 2,
    "title": "Buy groceries",
    "description": "Milk, bread, eggs, and fruits",
    "completed": false,
    "createdAt": "2025-06-26T11:00:00.000Z",
    "updatedAt": "2025-06-26T11:00:00.000Z"
  }
}
```

#### Update Todo
```http
PUT /api/todos/:id
```

**Parameters:**
- `id` (required): Todo item ID

**Request Body:**
```json
{
  "title": "string (optional)",
  "description": "string (optional)",
  "completed": "boolean (optional)"
}
```

**Example Request:**
```json
{
  "title": "Buy groceries - Updated",
  "completed": true
}
```

**Response:**
```json
{
  "success": true,
  "message": "Todo updated successfully",
  "data": {
    "id": 2,
    "title": "Buy groceries - Updated",
    "description": "Milk, bread, eggs, and fruits",
    "completed": true,
    "createdAt": "2025-06-26T11:00:00.000Z",
    "updatedAt": "2025-06-26T12:00:00.000Z"
  }
}
```

#### Delete Todo
```http
DELETE /api/todos/:id
```

**Parameters:**
- `id` (required): Todo item ID

**Response:**
```json
{
  "success": true,
  "message": "Todo deleted successfully"
}
```

### Error Responses

#### 400 Bad Request
```json
{
  "success": false,
  "error": "Bad Request",
  "message": "Title is required"
}
```

#### 404 Not Found
```json
{
  "success": false,
  "error": "Not Found",
  "message": "Todo not found"
}
```

#### 500 Internal Server Error
```json
{
  "success": false,
  "error": "Internal Server Error",
  "message": "Something went wrong"
}
```

## Usage Examples

### JavaScript (Fetch API)

```javascript
// Get all todos
fetch('http://localhost:3000/api/todos')
  .then(response => response.json())
  .then(data => console.log(data));

// Create new todo
fetch('http://localhost:3000/api/todos', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    title: 'New Task',
    description: 'Task description'
  })
})
.then(response => response.json())
.then(data => console.log(data));

// Update todo
fetch('http://localhost:3000/api/todos/1', {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    completed: true
  })
})
.then(response => response.json())
.then(data => console.log(data));

// Delete todo
fetch('http://localhost:3000/api/todos/1', {
  method: 'DELETE'
})
.then(response => response.json())
.then(data => console.log(data));
```

### cURL Examples

```bash
# Get all todos
curl -X GET http://localhost:3000/api/todos

# Create new todo
curl -X POST http://localhost:3000/api/todos \
  -H "Content-Type: application/json" \
  -d '{"title": "New Task", "description": "Task description"}'

# Update todo
curl -X PUT http://localhost:3000/api/todos/1 \
  -H "Content-Type: application/json" \
  -d '{"completed": true}'

# Delete todo
curl -X DELETE http://localhost:3000/api/todos/1
```

## Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
PORT=3000
NODE_ENV=development
```

### Server Configuration

The server can be configured by modifying the main server file:

```javascript
const PORT = process.env.PORT || 3000;
const app = express();

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// CORS configuration (if needed)
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type');
  next();
});
```

## Development

### Project Structure
```
Todo_API/
├── server.js          # Main server file
├── package.json       # Dependencies and scripts
├── package-lock.json  # Lock file
├── .env              # Environment variables
├── README.md         # Project documentation
└── routes/           # Route handlers (if organized)
    └── todos.js
```

### Testing

#### Manual Testing with Postman
1. Import the API endpoints into Postman
2. Test each endpoint with various data inputs
3. Verify response formats and status codes

#### Unit Testing (Recommended)
```bash
npm install --save-dev jest supertest
```

Example test structure:
```javascript
const request = require('supertest');
const app = require('./server');

describe('Todo API', () => {
  test('GET /api/todos should return all todos', async () => {
    const response = await request(app).get('/api/todos');
    expect(response.status).toBe(200);
    expect(response.body.success).toBe(true);
  });
});
```

## Deployment

### Local Development
```bash
npm start
# or
node server.js
```

### Production Deployment


## Security Considerations

### Recommended Enhancements
- **Input Validation**: Use libraries like Joi or express-validator
- **Rate Limiting**: Implement rate limiting to prevent abuse
- **Authentication**: Add JWT or session-based authentication
- **HTTPS**: Use HTTPS in production
- **Environment Variables**: Store sensitive data in environment variables
- **CORS**: Configure CORS properly for production

### Example Security Middleware
```javascript
const rateLimit = require('express-rate-limit');
const helmet = require('helmet');

// Security headers
app.use(helmet());

// Rate limiting
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});
app.use(limiter);
```

## Troubleshooting

### Common Issues

1. **Port Already in Use**
   ```bash
   Error: listen EADDRINUSE :::3000
   ```
   Solution: Change the port or kill the process using port 3000

2. **Module Not Found**
   ```bash
   Error: Cannot find module 'express'
   ```
   Solution: Run `npm install express`

3. **JSON Parsing Error**
   ```bash
   SyntaxError: Unexpected token in JSON
   ```
   Solution: Ensure request body is valid JSON and Content-Type header is set

### Debug Mode
```bash
DEBUG=* node server.js
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

For questions, issues, or contributions:
- **GitHub Issues**: Create an issue in the repository
- **Email**: Contact the maintainer
- **Documentation**: Refer to this documentation for API usage

## Changelog

### Version 1.0.0
- Initial release
- Basic CRUD operations for todos
- RESTful API endpoints
- JSON response format

## Future Enhancements

- User authentication and authorization
- Todo categories and tags
- Due dates and reminders
- File attachments
- Search and filtering
- Pagination for large datasets
- Real-time updates with WebSockets
- Database integration (MongoDB, PostgreSQL)
- API versioning
- Comprehensive test suite
