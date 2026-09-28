# Database Design - SeizeVoice

## Entities and Tables

### Users

| Field              | Type     | Description                |
| ------------------ | -------- | -------------------------- |
| user_id            | INT (PK) | Unique identifier          |
| anonymous_username | VARCHAR  | Public-facing display name |
| email              | VARCHAR  | Login email (private)      |
| password_hash      | VARCHAR  | Encrypted password         |
| created_at         | DATETIME | Account creation date      |

### Communities

| Field        | Type                      | Description                    |
| ------------ | ------------------------- | ------------------------------ |
| community_id | INT (PK)                  | Unique identifier              |
| name         | VARCHAR                   | Community name                 |
| description  | TEXT                      | Short description of the topic |
| created_by   | INT (FK -> Users.user_id) | Creator of the community       |
| created_at   | DATETIME                  | Creation date                  |

### Community_Members

| Field         | Type                                 | Description       |
| ------------- | ------------------------------------ | ----------------- |
| membership_id | INT (PK)                             | Unique identifier |
| user_id       | INT (FK -> Users.user_id)            | Member            |
| community_id  | INT (FK -> Communities.community_id) | Community joined  |
| joined_at     | DATETIME                             | Date joined       |

### Posts

| Field        | Type                                 | Description                     |
| ------------ | ------------------------------------ | ------------------------------- |
| post_id      | INT (PK)                             | Unique identifier               |
| community_id | INT (FK -> Communities.community_id) | Community it belongs to         |
| user_id      | INT (FK -> Users.user_id)            | Author (shown anonymously)      |
| title        | VARCHAR                              | Post title                      |
| body         | TEXT                                 | Post content                    |
| score        | INT                                  | Net votes (upvotes - downvotes) |
| created_at   | DATETIME                             | Date posted                     |

### Comments

| Field      | Type                      | Description                |
| ---------- | ------------------------- | -------------------------- |
| comment_id | INT (PK)                  | Unique identifier          |
| post_id    | INT (FK -> Posts.post_id) | Post being commented on    |
| user_id    | INT (FK -> Users.user_id) | Author (shown anonymously) |
| body       | TEXT                      | Comment content            |
| created_at | DATETIME                  | Date commented             |

### Votes

| Field      | Type                      | Description         |
| ---------- | ------------------------- | ------------------- |
| vote_id    | INT (PK)                  | Unique identifier   |
| user_id    | INT (FK -> Users.user_id) | Voter               |
| post_id    | INT (FK -> Posts.post_id) | Post being voted on |
| vote_type  | ENUM('up','down')         | Upvote or downvote  |
| created_at | DATETIME                  | Date voted          |

## Relationships

- One User can join many Communities (via Community_Members)
- One Community has many Posts
- One Post has many Comments
- One Post has many Votes (one per User, enforced by unique constraint
  on user_id + post_id)
