## Authentication System

### Authentication Strategies

| Strategy         | Description       | Provider |
| ---------------- | ----------------- | -------- |
| **Local**        | Email + Password  | LOCAL    |
| **Google OAuth** | Login with Google | GOOGLE   |

### JWT Token Flow

```typescript
// Access Token (15 min expiration)
{
  sub: userId,
  email: user.email,
  role: user.role,
  iat: timestamp,
  exp: timestamp + 15min
}

// Refresh Token (7 days expiration)
{
  sub: userId,
  type: 'refresh',
  iat: timestamp,
  exp: timestamp + 7days
}
```

### Refresh Token Flow

```mermaid
sequenceDiagram
    participant Client
    participant API
    participant DB

    Client->>API: Request with expired accessToken
    API-->>Client: 401 Unauthorized

    Client->>API: POST /auth/refresh with refreshToken
    API->>DB: Verify refreshToken hash
    DB-->>API: Token valid
    API->>API: Generate new accessToken
    API->>DB: Update refreshToken hash
    API-->>Client: New tokens

    Client->>API: Request with new accessToken
    API-->>Client: Successful response
```

### Authorization Guards

| Guard             | Purpose              |
| ----------------- | -------------------- |
| `JwtAuthGuard`    | Validates JWT token  |
| `RolesGuard`      | Verifies user role   |
| `GoogleAuthGuard` | Handles Google OAuth |

### Custom Decorators

```typescript
// Get user from request
@GetUser() user: User
@GetUser('id') userId: string

// Define allowed roles
@Roles(UserRole.ADMIN, UserRole.SELLER)

// Mark endpoint as public
@Public()
```
