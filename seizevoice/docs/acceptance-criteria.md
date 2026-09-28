# Acceptance Criteria - SeizeVoice

## Feature 1: Community Management

- Given a logged-in user, when they click "Create Community" and enter
  a valid name, then a new community is created and visible in the
  community list.
- Given an existing community, when a user clicks "Join," then they
  become a member and can post within that community.

## Feature 2: Anonymous Posting

- Given a user creating a post, when they submit it, then the post
  displays an anonymous username instead of their real name.
- Given two posts from the same anonymous user, when viewed by other
  users, then their real identity must not be visible or inferable.

## Feature 3: Voting System

- Given a visible post, when a user clicks upvote, then the post's
  score increases by 1 and the user cannot upvote the same post twice.
- Given a visible post, when a user clicks downvote, then the post's
  score decreases by 1.
- Given a community feed, when posts are displayed, then they are
  sorted from highest score to lowest by default.

## Feature 4: Post Creation

- Given a user inside a community, when they submit a post with a
  title and body text, then the post appears in that community's feed
  immediately.
- Given an empty title field, when a user tries to submit, then the
  system prevents submission and shows an error message.

## Feature 5: Comment System

- Given an existing post, when a user submits a comment, then the
  comment appears below the post in chronological order.
